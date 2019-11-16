# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network :forwarded_port, guest: 80, host: 8880
  config.vm.network :forwarded_port, guest: 3000, host: 8881
  config.vm.network "private_network", ip: "192.168.1.22"
  config.vm.provision "shell" do |s|
    ssh_public_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_public_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_public_key} >> /root/.ssh/authorized_keys
      apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
      sudo sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger bionic main > /etc/apt/sources.list.d/passenger.list'
      apt-get update
      apt-get upgrade -y
      apt-get install -y aptitude
    SHELL
  end
  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
end
