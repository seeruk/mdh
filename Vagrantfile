# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# Change these to suite your needs / machine
CPUS   = ENV["OCH_CPUS"] || 4
MEMORY = ENV["OCH_MEMORY"] || 4096

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "osx-container-host" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.hostname = "container-host"

    node.vm.provider "virtualbox" do |v|
      v.name = "osx-container-host"

      v.cpus   = CPUS
      v.memory = MEMORY

      v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on" ]
      v.customize [ "modifyvm", :id, "--natdnsproxy1", "on" ]
    end

    node.vm.network "private_network", ip: "192.168.200.2"

    node.nfs.map_uid = Process.uid
    node.nfs.map_gid = Process.gid

    node.vm.synced_folder "/Users", "/Users", type: "nfs",
      :mount_options => [ "actimeo=2" ]

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/ansible/container_host.yml"
    end
  end
end
