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
  config.vm.provider "virtualbox" do |v|
    v.cpus = 1 
    v.memory = 256
  end

  config.vm.define "lb" do |lb|
    lb.vm.box = "centos/7"
    lb.vm.hostname = "lb"
    lb.vm.network "private_network", ip: '10.10.10.10'
    lb.vm.provision "shell",
      inline: $sudo
  end

  config.vm.define "redis" do |redis|
    redis.vm.box = "centos/7"
    redis.vm.hostname = "redis"
    redis.vm.network "private_network", ip: '10.10.20.11'
    redis.vm.provision "shell",
      inline: $sudo
  end

  (1..2).each do |i|
    config.vm.define "web-#{i}" do |web|
      web.vm.box = "centos/7"
      web.vm.hostname = "web-#{i}"
      web.vm.network "private_network", ip: "10.10.30.#{10 + i}"
      web.vm.provision "shell",
        inline: $sudo
    end
  end


  (1..2).each do |i|
    config.vm.define "db-#{i}" do |db|
      db.vm.box = "centos/7"
      db.vm.hostname = "db-#{i}"
      db.vm.network "private_network", ip: "10.10.40.#{10 + i}"
      db.vm.provision "shell",
        inline: $sudo
    end
  end
end
