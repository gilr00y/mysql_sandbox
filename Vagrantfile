# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  MYSQL_DEST = '/mysql-server'
  config.vm.box = "ubuntu/vivid64"
  config.vm.synced_folder 'mysql-server', MYSQL_DEST
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision 'shell', inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install build-essential bison cmake libncurses5-dev
    wget http://sourceforge.net/projects/boost/files/boost/1.58.0/boost_1_58_0.tar.gz
    tar -xzvf boost_1_58_0.tar.gz
    cd boost_1_58_0
    ./bootstrap.sh && sudo ./b2 --prefix=/usr/include
    sudo mv boost /usr/include
    cd #{MYSQL_DEST} && cmake .
  SHELL

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"
end
