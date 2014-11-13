# -*- mode: ruby -*-
# vi: set ft=ruby :

# PLEASE NOTE:
# You will need the plugins listed below for this VM to function correctly.
# Please also note that the bindfs plugin does make performance a little slower
# but is necessary for permission in Docker containers to work as expected.
#
# $ vagrant plugin install vagrant-bindfs

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
      create_as_user: true,
      perms: "u=u:g=g:o=o"

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/ansible/container_host.yml"
    end
  end
end
