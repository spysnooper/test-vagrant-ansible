# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"
  config.ssh.insert_key = false

  config.vm.provider :libvirt do |libvirt|
    libvirt.storage_pool_name = "maquinas_virtuales-1"
    #libvirt.connect_via_ssh = true
  end
  
  config.vm.define "node1" do |node|
    node.vm.hostname = "node1.dev"
    node.vm.network :private_network, ip: "192.168.121.101"
  end
  
  config.vm.define "node2" do |node|
    node.vm.hostname = "node2.dev"
    node.vm.network :private_network, ip: "192.168.121.102"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "./ansible/playbook.yml"
    ansible.inventory_path = "./ansible/inventory"
    ansible.limit = "all"
  end

end
