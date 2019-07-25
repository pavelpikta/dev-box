# dev-box

This repository contains an Ansible provisioned Centos based VM for using with Vagrant.  
It's main use is to create on Windows machine Linux virtual machine to developing and testing ansible roles.  

## Setup Instructions

1. Install [Virtualbox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/).
2. Install `vagrant-vbguest` plugin. Run command `vagrant plugin install vagrant-vbguest`
3. Clone this repository and cd into it.
4. Configure the necessary variables in [`vars.yml`](vars.yml)  
**Important**: The synchronization folder `sync_fodler` should contain a repository `dev-box`
5. Run `vagrant up`

## Variables

### Vagrant machine settings
```yaml
box: 'centos/7'
name: 'Centos 7'
hostname: 'devbox'
cpu: '2'
ram: '2048'
sync_fodler: 'C:/Workspace'
```

### Ansible local provisioner variables

Read more about Vagrant Ansible provisioners:
* [Ansible and Vagrant](https://www.vagrantup.com/docs/provisioning/ansible_intro.html)
* [Ansible Local Provisioner](https://www.vagrantup.com/docs/provisioning/ansible_local.html)
* [Shared Ansible Options](https://www.vagrantup.com/docs/provisioning/ansible_common.html)

```yaml
ansible_folder: '/vagrant/dev-box/ansible/'
ansible_install_mode: 'pip'
ansible_version: '2.8.2'
ansible_become: true
ansible_playbook: 'playbook.yml'
ansible_inventory_path: 'host.yml'
ansible_config_file: 'ansible.cfg'
ansible_limit: 'localhost'
ansible_galaxy_role_file: 'requirements.yml'
ansible_galaxy_roles_path: 'roles'
ansible_verbose: false
```


### Ansible playbook and roles variables #
```yaml
configure_system: true
configure_env: true
packages:
  - bash-completion
  - bash-completion-extras
  - git
  - nano
  - sshpass
  - wget
tools:
  - cookiecutter
  - molecule
  - ansible-lint
  - docker
  - paramiko
  - pywinrm
  - pywinrm[credssp]
  - pywinrm[ntlm]
  - virtualenv
environment_vars:
  ANSIBLE_LIBRARY: ~/.ansible/plugins/modules
  ANSIBLE_NOCOLOR: false
  ANSIBLE_HOST_KEY_CHECKING: false
  ANSIBLE_FORCE_COLOR: true
  ANSIBLE_SSH_PIPELINING: true
  ANSIBLE_LOAD_CALLBACK_PLUGINS: true
  ANSIBLE_STDOUT_CALLBACK: debug
  ANSIBLE_CALLBACK_WHITELIST: profile_tasks, timer
  ANSIBLE_GATHERING: smart
docker_installation: true
docker_users:
  - vagrant
docker_daemon_opts: '-H fd:// -H unix:///var/run/docker.sock -H tcp://0.0.0.0:2376'
docker_daemon_config:
  storage-driver: overlay2
```
