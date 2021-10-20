Vagrant.configure("2") do |config|
  config.vm.box ="ubuntu/bionic64"
  config.vm.boot_timeout = 1200
  config.vm.provider "virtualbox" do |vb|
    vb.memory ="1024"
  end 

  # Configure provisioners on the machine
  config.vm.provision :docker
  config.vm.provision :docker_compose
  
  # Configure server "ci-server"
   config.vm.define "ci-server" do |ciserver| 
    ciserver.vm.network "private_network", ip: '192.168.33.65'
    ciserver.vm.hostname = "ci-server"
  end
  
  #Configure server "server-2"
  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: "192.168.33.66"
    server2.vm.hostname = "server-2"
    server2.vm.provision :docker_compose, yml: "/vagrant/MachineLearning/docker-compose.yml", rebuild: true, run: "always"
  end
end