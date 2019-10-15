# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

# Define the host "master"
  config.vm.define "master" do |machine|
    machine.vm.network "private_network", ip: "192.168.69.11"
    # Create config
    machine.vm.provider "virtualbox" do |m|
        m.customize ["modifyvm", :id, "--name", "master"]
        m.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        m.customize ["modifyvm", :id, "--memory", 256]
    end
  end

  # Define the host "slave1"
  config.vm.define "slave1" do |machine|
    # Create a private network of hosts
    machine.vm.network "private_network", ip: "192.168.69.12"
    # Create config
    machine.vm.provider "virtualbox" do |s|
        s.customize ["modifyvm", :id, "--name", "slave1"]
        s.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        s.customize ["modifyvm", :id, "--memory", 256]
    end
  end

  config.vm.provision :ansible_local do |ansible|
    ansible.become   = true
    ansible.playbook = 'ansible-bigdata-playbook.yml'
    ansible.verbose  = 'vvv'
    ansible.install  = true
    ansible.limit    = 'all'
    ansible.inventory_path = './inventory'
  end
end
