# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "container-host" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.hostname = "container-host"

    node.vm.provider "virtualbox" do |v|
      v.name = "container-host"

      v.memory = 4096
      v.cpus = 4
    end

    node.vm.network "private_network", ip: "192.168.200.2"
    node.vm.network "forwarded_port", guest: 80, host: 80
    node.vm.network "forwarded_port", guest: 443, host: 443
    node.vm.network "forwarded_port", guest: 3306, host: 3306

    node.vm.synced_folder "../../", "/opt/git/", type: "nfs"

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/ansible/container_host.yml"
    end
  end
end
