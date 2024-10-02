# -*- mode: ruby -*-
# vi: set ft=ruby :

machines = {
  "master" => {"image" => "bento/ubuntu-22.04", "cpu" => "1", "memory" => "1024", "ip" => "100"},
  "node01" => {"image" => "bento/ubuntu-22.04", "cpu" => "1", "memory" => "1024", "ip" => "200"},
}

Vagrant.configure("2") do |config|
  machines.each do |name, value|
    config.vm.define "#{name}" do |machine|
    
      machine.vm.hostname = "#{name}"
      machine.vm.box = "#{value["image"]}"
      machine.vm.network "private_network", ip: "10.10.10.#{value["ip"]}"
      
      machine.vm.provider "virtualbox" do |vbox|
        vbox.name = "#{name}"
        vbox.memory = value["memory"]
        vbox.cpus = value["cpu"]
      end

      machine.vm.provision "shell", path: "install_docker.sh"
      if "#{name}" == "master"
        machine.vm.provision "shell", path: "manager.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end

    end
  end
end
