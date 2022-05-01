# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "wate/debian-11"
  # config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 1234, host: 1234
  config.vm.network "private_network", ip: "192.168.56.234"
  # config.vm.synced_folder "./data", "/vagrant_data"

  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #   vb.memory = "1024"
  # end
  config.vm.provision "ansible_local" do |ansible|
    ansible.become = true
    ansible.compatibility_mode = "2.0"
    ansible.provisioning_path = "/vagrant/provision"
    ansible.playbook = "playbook.yml"
    ansible.config_file = "/vagrant/provision/ansible.cfg"
    ansible.extra_vars = ansible_extra_vars
  end
end
