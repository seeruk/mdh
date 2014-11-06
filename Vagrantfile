# -*- mode: ruby -*-
# vi: set ft=ruby :

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
    node.nfs.map_uid = Process.uid
    node.nfs.map_gid = Process.gid

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/ansible/container_host.yml"
    end
  end
end
