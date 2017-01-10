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
    #node.hostsupdater.aliases = ["node1.example.com", "node1.example.local"]
    #node.vm.network "private_network", ip: "192.168.121.101"
    node.vm.provision "shell" do |s|
      s.inline = "sudo nmcli con mod 'System eth0' ipv4.method manual ipv4.addresses 192.168.121.101/24 ipv4.gateway 192.168.121.1 ipv4.dns 192.168.121.1; sudo nmcli con up 'System eth0'"
    end
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = './ansible/playbook.yml'
      ansible.inventory_path = './ansible/inventory'
      ansible.sudo = true
      ansible.limit = 'node1'
      ansible.verbose = 'vvvv'
    end
  end
  
  config.vm.define "node2" do |node|
    node.vm.hostname = "node2.dev"
    #node.hostsupdater.aliases = ["node2.example.com", "node2.example.local"]
    #node.vm.network "private_network", ip: "192.168.121.102"
    node.vm.provision "shell" do |s|
      s.inline = "sudo nmcli con mod 'System eth0' ipv4.method manual ipv4.addresses 192.168.121.102/24 ipv4.gateway 192.168.121.1 ipv4.dns 192.168.121.1; sudo nmcli con up 'System eth0'"
    end
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = './ansible/playbook.yml'
      ansible.inventory_path = './ansible/inventory'
      ansible.sudo = true
      ansible.limit = 'node2'
      ansible.verbose = 'vvvv'
    end
  end

end
