# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"
  #config.ssh.insert_key = false

  config.vm.provider :libvirt do |libvirt|
    libvirt.storage_pool_name = "maquinas_virtuales-1"
    #libvirt.connect_via_ssh = true
  end
  
  config.vm.define "node1" do |node|
    node.vm.hostname = "node1"
  end
  
  config.vm.define "node2" do |node|
    node.vm.hostname = "node2"
  end
    
  config.vm.provision "ansible" do |ansible|
      ansible.groups = {
          "all-nodes" => ["node1", "node2"],
      }
      ansible.playbook = './ansible/playbook.yml'
      ansible.sudo = true
      ansible.verbose = 'vvvv'
  end
end
