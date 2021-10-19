# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box ="ubuntu/bionic64"
  # config.vm.boot_timeout = 600
  config.vm.provider "virtualbox" do |vb|
    vb.memory ="1024"
  end 

  # Configure provisioners on the machine
  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.define "server-1" do |server1|
    server1.vm.network "private_network", ip: '192.168.33.50'
    server1.vm.hostname = "server-1"
    server1.vm.provision "shell", inline: <<-SHELL
      apt-get -y update
      apt-get -y install nginx
      service nginx start
    SHELL
  end

  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.33.51'
    server2.vm.hostname = "server-2"
  end

end