=begin
 * This file is part of OSXContainerHost
 *
 * (c) Elliot Wright <elliot@elliotwright.co>
 *
 * For full copyright and license information, please view the LICENSE file
 * distributed with this source code.
=end

VAGRANTFILE_API_VERSION = '2'

# Configuration
CPUS    = 8
MEMORY  = 4096
MNT_DIR = '/Users/seer/git/projects'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define 'container-host' do |node|
    node.vm.box = 'ubuntu/trusty64'
    node.vm.hostname = 'container-host'

    node.vm.provider 'virtualbox' do |v|
      v.name = 'container-host'

      v.cpus   = CPUS
      v.memory = MEMORY
    end

    node.vm.network 'private_network', ip: '192.168.200.2'

    node.vm.synced_folder MNT_DIR, MNT_DIR, type: 'rsync',
      owner: 'vagrant',
      group: 'vagrant'

    node.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'provisioning/ansible/container_host.yml'
    end
  end
end
