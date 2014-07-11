# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.network :forwarded_port, guest: 8777, host: 8777
  config.vm.network :private_network, ip: "10.0.0.10"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.define "geotrellis-playground" do |node|
    node.vm.hostname = "geotrellis.playground.dev"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.inventory_path = "provisioning/hosts"
    ansible.verbose = "v"
    ansible.limit = 'all'
  end
  
end
