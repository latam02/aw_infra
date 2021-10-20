$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love Linux"
date > ~/vagrant_provisioned_at

SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box ="ubuntu/bionic64"
  # config.vm.boot_timeout = 600
  config.vm.provider "virtualbox" do |vb|
    vb.memory ="1024"
  end 

  # Configure provisioners on the machine
  config.vm.provision :docker
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.provision :file, source: "file.txt", destination: "file.txt"
  
  config.vm.define "server-1" do |dockerserver|
    dockerserver.vm.network "private_network", ip: '192.168.33.60'
    dockerserver.vm.hostname = "dockerserver"
    config.vm.provision :file, source: "Folder", destination: "Folder"
    dockerserver.vm.provision "shell", inline: "echo Hi Class!"
    dockerserver.vm.provision "shell", inline: $script
    dockerserver.vm.provision "shell" do |s|
      s.inline = "echo $1"
      s.args = ["AT", "Class!"]
      end
     dockerserver.vm.provision "docker" do |d|
      d.run "hello-world"
      end
  end
end