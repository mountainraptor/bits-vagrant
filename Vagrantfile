# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network :private_network, ip: "192.168.37.13"
  config.vm.hostname = "bits.dev"
  config.vm.synced_folder "../bits", "/opt/bits"
  # config.vm.synced_folder "../modules", "/opt/bits-data/base/modules/modules"

  config.vm.provider :virtualbox do |vb|
    vb.memory = 1024
    vb.cpus = 1
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
    vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end
end
