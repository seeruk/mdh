# -*- mode: ruby -*-
# vi: set ft=ruby :

# Ensure that you have the vagrant-triggers plugin installed:
#
# $ vagrant plugin install vagrant-triggers

VAGRANTFILE_API_VERSION = "2"

# Change these to suite your needs / machine
CPUS   = 4
MEMORY = 4096

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "container-host" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.hostname = "container-host"

    node.vm.provider "virtualbox" do |v|
      v.name = "container-host"

      v.cpus   = CPUS
      v.memory = MEMORY
    end

    node.vm.network "private_network", ip: "192.168.200.2"

    node.vm.synced_folder "/Users", "/Users", type: "nfs"

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/ansible/container_host.yml"
    end

    node.trigger.after :command, :option => "value" do
      run "export DOCKER_HOST=tcp://192.168.200.2:2375"
    end
  end
end
