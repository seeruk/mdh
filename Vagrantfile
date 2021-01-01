# -*- mode: ruby -*-
# vi: set ft=ruby :

# Change these to suite your needs / machine
CPUS   = ENV["MDH_CPUS"] || 4
MEMORY = ENV["MDH_MEMORY"] || 4096

Vagrant.require_version ">= 2.2"
Vagrant.configure("2") do |config|
  config.vm.define "mdh" do |node|
    node.vm.box = "ubuntu/focal64"
    node.vm.hostname = "mdh"

    node.vm.provider "virtualbox" do |v|
      v.name = "mdh"
      v.cpus   = CPUS
      v.memory = MEMORY
    end

    node.vm.network "private_network", ip: "192.168.200.2"

    node.vm.provision "docker" do |d|
      # We just want Docker installed
    end
  end
end
