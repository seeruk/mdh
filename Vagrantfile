# -*- mode: ruby -*-
# vi: set ft=ruby :

# PLEASE NOTE:
# You will need the vagrant-triggers and vagrant-exec plugins installed for this
# environment to work properly.
#
# $ vagrant plugin install vagrant-triggers
# $ vagrant plugin install vagrant-exec

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

    node.nfs.map_uid = Process.uid
    node.nfs.map_gid = Process.gid

    node.vm.synced_folder "/Users", "/Users.tmp", type: "nfs"
    node.bindfs.bind_folder "/Users.tmp", "/Users",
      create_as_user: true

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/ansible/container_host.yml"
    end

    node.trigger.after :up do
      # Stop standard Docker daemon and start remote Docker daemon
      # @TODO: Make this happen automatically when the VM is booted, in the VM!
      run 'vagrant exec sudo service docker stop'
      run 'vagrant exec sudo service dockerd start'
    end
  end
end
