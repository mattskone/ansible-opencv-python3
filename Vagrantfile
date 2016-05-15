# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.verbose = "vv"
    ansible.playbook = "playbook.yml"
  end
end

