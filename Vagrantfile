# -*- mode: ruby -*-
# by eddie@5xruby.tw

Vagrant.configure("2") do |config|
  # vm(ubuntu 18.04 LTS)
  config.vm.box = "ubuntu/bionic64"

  # network settings
  config.vm.network :forwarded_port, guest: 80, host: 8880
  config.vm.network :forwarded_port, guest: 3000, host: 8881
  config.vm.network "private_network", ip: "192.168.1.22"

  # hardware settings
  config.vm.provider "virtualbox" do |v|
    v.name = "CCH_v1"
    v.gui = false
    v.memory = 4096
    v.cpus = 4
    v.customize ["modifyvm", :id, "--audio", "none"]  # disable audio
  end

  config.vm.provision "shell" do |s|
    ssh_public_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_public_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_public_key} >> /root/.ssh/authorized_keys
      apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
      sudo sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger bionic main > /etc/apt/sources.list.d/passenger.list'
      apt-get install -y aptitude
    SHELL
  end
end

