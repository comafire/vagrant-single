# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|

  config.vm.define "s01" do |host|
    host.vm.box = "ubuntu/xenial64" # ubuntu 16.04 LTS
    host.vm.hostname = "s01"
    host.vm.network "public_network", ip: "192.168.0.50"
    #host.vm.network "private_network", ip: "10.0.1.1"
    host.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.cpus = 4
      vb.memory = "16384"
    end
    host.disksize.size = '128GB'
    host.vm.synced_folder "../../../", "/home/vagrant/st-kilda-pier", owner: "vagrant", group: "vagrant"

    # SSH enable password login
    host.vm.provision "shell", inline: "sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config"
    host.vm.provision "shell", inline: "service ssh restart"
    # Install Ansible
    host.vm.provision "shell", inline: "apt-get update"
    host.vm.provision "shell", inline: "apt-get install software-properties-common"
    host.vm.provision "shell", inline: "apt-add-repository --yes --update ppa:ansible/ansible"
    host.vm.provision "shell", inline: "apt-get install -y ansible"
    host.vm.provision "shell", inline: "sed -i -e 's/#host_key_checking = False/host_key_checking = False/g' /etc/ansible/ansible.cfg"    
  end

end
