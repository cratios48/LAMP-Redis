# -*- mode: ruby -*-
# vi: set ft=ruby :

$sudo = <<SCRIPT
sudo yum install -y vim
sudo useradd jjh
sudo mkdir /home/jjh/.ssh
sudo cp -r /vagrant/id_rsa.pub /home/jjh/.ssh/authorized_keys
sudo chown -R jjh:jjh /home/jjh
sudo echo '%jjh ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/jjh
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "lb" do |lb|
    lb.vm.hostname = "lb"
    #lb.vm.network "private_network", ip: '10.10.10.10'
    lb.vm.provider "virtualbox" do |v|
      v.cpus = 1
      v.memory = 256
    end
    lb.vm.provision "shell",
      inline: "$sudo"
  end

  config.vm.define "redis" do |redis|
    redis.vm.hostname = "redis"
    #redis.vm.network "private_network", ip: '10.10.10.10'
    redis.vm.provider "virtualbox" do |v|
      v.cpus = 1
      v.memory = 256
    end
    redis.vm.provision "shell",
      inline: "$sudo"
  end

  (1..2).each do |i|
    config.vm.define "web-${i}" do |web|
      web.vm.hostname = "web-${i}"
      #web.vm.network "private_network", ip: '10.10.10.20'
      web.vm.provider "virtualbox" do |v|
        v.cpus = 1
        v.memory = 256
      end
      web.vm.provision "shell",
        inline: "$sudo"
    end
  end


  (1..2).each do |i|
    config.vm.define "db-${i}" do |db|
      db.vm.hostname = "db-${i}"
      #db.vm.network "private_network", ip: '10.10.10.20'
      db.vm.provider "virtualbox" do |v|
        v.cpus = 1
        v.memory = 256
      end
      db.vm.provision "shell",
        inline: "$sudo"
    end
  end
end
