# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'.freeze

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'geerlingguy/ubuntu1804'
  # Vagrant instance name displayed in console
  config.vm.define 'mysql-vm'

  config.vm.network :private_network, ip: '192.168.5.99'
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.hostname = "mysql.dev"
  config.ssh.insert_key = false
  config.vm.synced_folder './', '/vagrant/src', type: "nfs",
    mount_options: ['rw', 'vers=3', 'tcp'],
    linux_nfs_options: ['rw', 'no_subtree_check', 'all_squash', 'async']

  config.vm.provider :virtualbox do |v|
    v.name = 'MySql-vm'
    v.memory = 1024
    v.cpus = 1
  end

  # Ansible provisioner.
  config.vm.provision :ansible do |ansible|
    ansible.compatibility_mode="2.0"
    ansible.playbook = 'provisioning/playbook.yml'
    ansible.inventory_path = "provisioning/inventory/dev_inventory"
    ansible.limit = "all"
    ansible.galaxy_role_file = "provisioning/requirements.yml"
    ansible.become = true
    ansible.extra_vars = {
      ansible_ssh_user: "vagrant",
      ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
    }
    # Enables passing of args to Ansible from Vagrant CLI
    # via the A_ARGS environment variable
    if ENV['A_ARGS']
      ansible.raw_arguments = Shellwords.shellsplit(ENV['A_ARGS'])
    end
  end
end
