# -*- mode: ruby -*-
# vi: set ft=ruby :
# Thanks to Lynn Root: https://gist.github.com/econchick/99699a6fee2eb44d13b0
 
Vagrant.configure("2") do |config|
  config.vm.box = "CentOS-6.4-VBox"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-64-x64-vbox4210.box"

  config.vm.define :kdc do |master|
    master.vm.network :forwarded_port, guest: 80, host: 8081
    master.vm.network :forwarded_port, guest: 443, host: 1443
    master.vm.network :private_network, ip: "192.168.19.15"
    master.vm.hostname = "kdc.openampere.com"
    master.vm.provision :ansible do |ansible|
      ansible.sudo = true
      ansible.inventory_path = "inventory.yml"
      ansible.playbook = "master.yml"
      ansible.verbose = "vv"
    end
  end

  config.vm.define :client do |client|
    client.vm.network :forwarded_port, guest: 80, host: 8888
    client.vm.network :forwarded_port, guest: 443, host: 2443
    client.vm.network :private_network, ip: "192.168.19.20"
    client.vm.hostname = "node1.openampere.com"
    client.vm.synced_folder "website/", "/var/www/website"
    client.vm.provision :ansible do |ansible|
      ansible.sudo = true
      ansible.inventory_path = "inventory.yml"
      ansible.playbook = "node1.yml"
      ansible.verbose = "vv"
    end
  end

end