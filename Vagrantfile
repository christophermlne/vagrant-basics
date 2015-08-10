# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # https://docs.vagrantup.com.
  config.vm.box = "hashicorp/precise64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 3000, host: 3000 

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    set -e
    sudo locale-gen en_US

    echo "=> updating and installing build-essential..."
    sudo apt-get update -qq && sudo apt-get install -y build-essential
    echo "=> installing libpq-dev..."
    sudo apt-get install -y libpq-dev > /dev/null
    echo "=> installing libxml2-dev and libxslt1-dev..."
    sudo apt-get install -y libxml2-dev libxslt1-dev > /dev/null
    echo "=> installing libqt4-webkit, libqt4-dev, and xvfb..."
    sudo apt-get install -y libqt4-webkit libqt4-dev xvfb > /dev/null
    echo "=> installing libsqlite3..."
    sudo apt-get install -y libsqlite3-dev > /dev/null
    echo "=> installing nodejs..."
    sudo apt-get install -y nodejs > /dev/null

    echo "=> installing git..."
    sudo apt-get install -y git > /dev/null

    # setup rbenv and ruby-build
    echo "=> attempting to install rbenv..."
    git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
    
    # Install ruby 2.1.2 and bundler
    export RBENV_ROOT="${HOME}/.rbenv"
    export PATH="${RBENV_ROOT}/bin:${PATH}"
    export PATH="${RBENV_ROOT}/shims:${PATH}"

    echo '=> installing Ruby 2.1.5...'
    rbenv install 2.1.5
    echo '=> setting global Ruby version to 2.1.5...'
    rbenv global 2.1.5

    echo '=> creating .gemrc file with skip documentation as default...'
    touch ~/.gemrc
    echo "gem: --no-rdoc --no-ri" >> ~/.gemrc
    gem install bundler
    rbenv rehash

    #echo '=> installing bundler and rails...'
    #gem install rails

    #echo '=> installing vim'
    #apt-get install -y vim
  SHELL
end
