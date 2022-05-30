# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "wate/debian-11"
  # config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 1234, host: 1234
  config.vm.network "forwarded_port", guest: 3306, host: 3306
  config.vm.network "forwarded_port", guest: 8025, host: 8025
  config.vm.network "private_network", ip: "192.168.56.234"

  ansible_extra_vars = {
    redmine_user: "vagrant",
    redmine_home: "/vagrant/redmine",
    redmine_mode: "development"
  }
  extra_var_file = File.expand_path(File.join(File.dirname(__FILE__), 'extra_vars.yml'))
  if File.exists?(extra_var_file)
    ansible_extra_vars.merge!(YAML.load_file(extra_var_file))
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.become = true
    ansible.compatibility_mode = "2.0"
    ansible.provisioning_path = "/vagrant/provision"
    ansible.playbook = "playbook.yml"
    ansible.config_file = "/vagrant/provision/ansible.cfg"
    ansible.extra_vars = ansible_extra_vars
  end
end
