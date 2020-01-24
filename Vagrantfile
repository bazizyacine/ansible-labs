# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Kubernetes Master Server
  config.vm.define "masterAnsible" do |kubemaster|
    kubemaster.vm.box = "centos/7"
    kubemaster.vm.hostname = "masterAnsible.m2i.form"
    kubemaster.vm.network "private_network", ip: "172.42.42.100"
    kubemaster.vm.provider "virtualbox" do |v|
      v.name = "masterAnsible"
      v.memory = 2048
      v.cpus = 2
    end
    kubemaster.vm.provision "shell", path: "bootstrap.sh"
  end

  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "workerAnsible#{i}" do |workernode|
      workernode.vm.box = "centos/7"
      workernode.vm.hostname = "workerAnsible#{i}.m2i.form"
      workernode.vm.network "private_network", ip: "172.42.42.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "workerAnsible#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      workernode.vm.provision "shell", path: "bootstrap.sh"
    end
  end

end
