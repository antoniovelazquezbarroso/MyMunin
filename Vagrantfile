# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure(2) do |config|

  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end


  config.vm.define "railsapp" do |railsapp|

    railsapp.vm.box = "geerlingguy/ubuntu1404"
    railsapp.vm.hostname = "railsapp"    
    railsapp.vm.network :private_network, ip: "192.168.2.60"
  end


  config.vm.define "control" do |control|

    control.vm.box = "geerlingguy/ubuntu1404"
    control.vm.hostname = "control"    
    control.vm.network :private_network, ip: "192.168.2.55"

    control.vm.provision "ansible" do |ansible|
      ansible.playbook = "configure.yml"
      ansible.inventory_path = "inventories/vagrant/inventory"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end

  end


end
