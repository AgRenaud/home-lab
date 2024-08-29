Ray Service Experiment
---

1. Install KubeRay Operator

```sh
helm repo add kuberay https://ray-project.github.io/kuberay-helm/
helm repo update

helm install kuberay-operator kuberay/kuberay-operator --version 1.1.1
```

2. Deploy Service

```sh
kubectl apply -f ray-service.sample.yml
```

3. Wait

Pods init may takes some times ..

4. Forward Dashboard

```sh
kubectl get services

kubectl port-forward svc/rayservice-sample-head-svc 8265:8265
```

5. Test endpoints

```sh
kubectl run curl --image=radial/busyboxplus:curl -i --tty

curl -X POST -H 'Content-Type: application/json' rayservice-sample-serve-svc:8000/calc/ -d '["ADD", 7]'
curl -X POST -H 'Content-Type: application/json' rayservice-sample-serve-svc:8000/calc/ -d '["MUL", 3]'
```

