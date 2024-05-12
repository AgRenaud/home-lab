Home Lab
================

# Getting Started

## Requirements:
- Python3
- Vagrant
- qemu

## Start a Lab

### Run VM cluster with vagrant

Create a VMs with `vagrant up`.

You should be able to connect to the VMs with `vagrant ssh <vm-name>`

### Provision VM with Ansible

First setup a python environment for `Ansible`.

```shell
python3 -m venv venv
source venv/bin/activate

pip install -r requirements/requirements.txt

# Then install ansible dependencies (Roles & collection)
ansible-galaxy role install -r requirements/requirements.yml

# Create a cluster
ansible-playbook -i inventory/local.yml playbooks/cluster.yml

# Fetch the kubeconfig file
ansible-playbook -i inventory/local.yml playbooks/operations/get_kubeconfig.yml
```

`playbooks/operations/get_kubeconfig.yml` will fetch cluster kubeconfig file `k3s.yaml`.

We can test that the cluster and all the nodes are ready thanks to `kubectl`.

```txt
$ export KUBECONFIG=k3s.yaml
$ kubectl get nodes -o wide

NAME              STATUS   ROLES                  AGE    VERSION        INTERNAL-IP       EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
node03-770d2d73   Ready    <none>                 95m    v1.29.4+k3s1   192.168.121.130   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.7.15-k3s1
node01-c421e57f   Ready    control-plane,master   100m   v1.29.4+k3s1   192.168.121.59    <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.7.15-k3s1
node02-d692201c   Ready    <none>                 96m    v1.29.4+k3s1   192.168.121.27    <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.7.15-k3s1
```
