# -*- mode: ruby -*-
# vi: set ft=ruby :
# Thanks to Lynn Root: https://gist.github.com/econchick/99699a6fee2eb44d13b0
 
Vagrant.configure("2") do |config|

  config.vm.box = "CentOS-6.4-VBox-NoCM"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-64-x64-vbox4210-nocm.box"

  config.vm.provider :virtualbox do |vb|
    vb.auto_nat_dns_proxy = false
  end

  config.vm.define :master do |master|
    master.vm.network :forwarded_port, guest: 80, host: 8081
    master.vm.network :forwarded_port, guest: 443, host: 1443
    master.vm.network :private_network, ip: "192.168.19.15"
    master.vm.hostname = "master.test.openampere.com"
    master.vm.synced_folder "certs/", "/etc/certs"
    master.vm.provision :ansible do |ansible|
      ansible.sudo = true
      ansible.inventory_path = "inventory.yml"
      ansible.playbook = "master.yml"
      ansible.verbose = "vv"
    end
  end

  #config.vm.define :node1 do |node1|
  #  node1.vm.network :forwarded_port, guest: 80, host: 8888
  #  node1.vm.network :forwarded_port, guest: 443, host: 2443
  #  node1.vm.network :private_network, ip: "192.168.19.20"
  #  node1.vm.hostname = "node1.test.openampere.com"
  #  node1.vm.synced_folder "website/", "/var/www/website"
  #  node1.vm.provision :ansible do |ansible|
  #    ansible.sudo = true
  #    ansible.inventory_path = "inventory.yml"
  #    ansible.playbook = "node1.yml"
  #    ansible.verbose = "vv"
  #  end
  #end

end