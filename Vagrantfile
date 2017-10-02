# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  # config.vm.network "forwarded_port", guest: 80, host: 4444
  # config.vm.network "public_network"

  config.vm.define "db1" do |db1|
    # db1.vm.network "forwarded_port", guest: 8080, host: 3456
    db1.vm.network "private_network", ip: "192.168.19.10"

    db1.vm.provider "virtualbox" do |vb|
      vb.name = "Galera 1"
      vb.memory = "512"
    end
  end

  config.vm.define "db2" do |db2|
    db2.vm.network "private_network", ip: "192.168.19.11"

    db2.vm.provider "virtualbox" do |vb|
      vb.name = "Galera 2"
      vb.memory = "512"
    end
  end

  config.vm.define "db3" do |db3|
    db3.vm.network "private_network", ip: "192.168.19.12"

    db3.vm.provider "virtualbox" do |vb|
      vb.name = "Galera 3"
      vb.memory = "512"
    end
  end

  config.vm.synced_folder ".", "/vagrant", type: "nfs"
  # config.vm.synced_folder "../web", "/var/www/web", owner: "vagrant", group: "vagrant"
  # config.vm.synced_folder "../blog", "/var/www/blog", owner: "vagrant", group: "vagrant"

  config.vm.provision "shell", inline: <<-SHELL
    sudo yum install epel-release -y
    sudo yum update -y
    sudo yum install ansible -y
  SHELL

  config.vm.provision "shell", inline: <<-SHELL
    cp /vagrant/ansible/keys/id_rsa /home/vagrant/.ssh
    cp /vagrant/ansible/keys/id_rsa.pub /home/vagrant/.ssh
    cd /home/vagrant/.ssh && sudo chown vagrant:vagrant id_rsa id_rsa.pub
    cd /home/vagrant/.ssh && sudo chmod 600 id_rsa id_rsa.pub
    cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL
end
