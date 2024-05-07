# -*- mode: ruby -*-
# vi: set ft=ruby :
#
#

workers = [
  { :hostname => "node01", :ip => "10.10.10.101", :memory => "2048", :cpus => 2 },
  { :hostname => "node02", :ip => "10.10.10.102", :memory => "1024", :cpus => 2 },
  { :hostname => "node03", :ip => "10.10.10.103", :memory => "1024", :cpus => 1 },
]

Vagrant.configure("2") do |config|
   workers.each do |conf|

    config.vm.define conf[:hostname] do |node|
      node.vm.box = "generic/ubuntu2204"
      node.vm.network "private_network", ip: conf[:ip], netmask: "255.255.255.0"

      node.vm.provider :libvirt do |libvirt|
        libvirt.driver = "qemu"
        libvirt.memory = conf[:memory]
        libvirt.cpus = conf[:cpus]
      end
    end
  end
end
