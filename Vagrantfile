# -*- mode: ruby -*-
# vi: set ft=ruby :

# Project Name
$project_name = "Bond"

# Check /etc/hosts and provision one ip
$ip_address = "192.168.4.18"

# Sets guest environment variables.
# @see https://github.com/hashicorp/vagrant/issues/7015
$set_environment_variables = <<SCRIPT
tee "/etc/profile.d/myvars.sh" > "/dev/null" <<EOF
# Ansible environment variables.
export ANSIBLE_RETRY_FILES_ENABLED=0
EOF
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.define $project_name do |i|
    i.vm.provider "virtualbox" do |v|
      v.name = $project_name
      v.memory = 2048
      v.cpus = 2
    end
    i.vm.hostname = $project_name
    i.vm.network "private_network", ip: $ip_address
    i.vm.network "private_network", ip: "192.168.4.10"
  end
#-------------------------------------------------------------------------------
# Provision
#-------------------------------------------------------------------------------
  config.vm.provision "shell", inline: $set_environment_variables, run: "always"
  config.vm.provision "shell", path: "scripts/bootstrap.sh"
  config.vm.provision "ansible_local" do |ansible|
      ansible.install = false
      ansible.provisioning_path = "/vagrant/ansible"
      ansible.playbook = "playbook.yml"
      ansible.become = true
      ansible.tags = ENV['ANSIBLE_TAGS']
      ansible.verbose = ENV['ANSIBLE_VERBOSE']
  end
end
