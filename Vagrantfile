# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

machine = YAML.load_file(File.join(File.dirname(__FILE__), 'vars.yml'))

Vagrant.configure("2") do |config|
  config.vm.box = machine['box']
  config.vm.hostname = machine['hostname']
  config.vm.network "public_network"
  config.vm.box_check_update = true
  config.vm.synced_folder machine['sync_fodler'], "/vagrant", type: "virtualbox", disabled: false, mount_options: ["dmode=775"]

  config.vm.provider "virtualbox" do |vb|
  vb.memory = machine['ram']
  vb.cpus = machine['cpu']
  vb.name = machine['name']
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.install_mode = machine['ansible_install_mode']
    ansible.version = machine['ansible_version']
    ansible.become = machine['ansible_become']
    ansible.playbook = machine['ansible_folder'] + machine['ansible_playbook']
    ansible.inventory_path = machine['ansible_folder'] + machine['ansible_inventory_path']
    ansible.config_file = machine['ansible_folder'] + machine['ansible_config_file']
    ansible.limit = machine['ansible_limit']
    ansible.galaxy_role_file = machine['ansible_folder'] + machine['ansible_galaxy_role_file']
    ansible.galaxy_roles_path = machine['ansible_folder'] + machine['ansible_galaxy_roles_path']
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
    ansible.verbose = machine['ansible_verbose']
  end
end
