# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.

Vagrant.configure("2") do |config|
  config.vm.define "raulbalanceador" do |raulbalanceador|
    raulbalanceador.vm.box = "generic/debian11"
    raulbalanceador.vm.hostname = "raulbalanceador"
    raulbalanceador.vm.network "private_network", ip: "192.168.5.10",
              virtualbox__intnet: "redbalanceador"
    raulbalanceador.vm.network "public_network"
    raulbalanceador.vm.provision "shell", path: "scriptbalanceador.sh"
  end
  config.vm.define "raulnginx" do |raulnginx|
    raulnginx.vm.box = "generic/debian11"
    raulnginx.vm.hostname = "raulnginx"
    raulnginx.vm.network "private_network", ip: "192.168.5.11",
              virtualbox__intnet: "redbalanceador"
    raulnginx.vm.network "private_network", ip: "192.168.10.21",
              virtualbox__intnet: "redmysql"
    raulnginx.vm.network "public_network"
    raulnginx.vm.provision "shell", path: "scriptnginx.sh"
  end
  config.vm.define "raulnginx2" do |raulnginx2|
    raulnginx2.vm.box = "generic/debian11"
    raulnginx2.vm.hostname = "raulnginx2"
    raulnginx2.vm.network "private_network", ip: "192.168.5.12",
              virtualbox__intnet: "redbalanceador"
    raulnginx2.vm.network "private_network", ip: "192.168.10.22",
              virtualbox__intnet: "redmysql"
    raulnginx2.vm.network "public_network"
    raulnginx2.vm.provision "shell", path: "scriptnginx.sh"
  end
  config.vm.define "raulnfs" do |raulnfs|
    raulnfs.vm.box = "generic/debian11"
    raulnfs.vm.hostname = "raulnfs"
    raulnfs.vm.network "private_network", ip: "192.168.5.13",
              virtualbox__intnet: "redbalanceador"
    raulnfs.vm.network "private_network", ip: "192.168.10.23",
              virtualbox__intnet: "redmysql"
    raulnfs.vm.network "public_network"
    raulnfs.vm.provision "shell", path: "scriptnfs.sh"
  end
  config.vm.define "raulmysql" do |raulmysql|
    raulmysql.vm.box = "generic/debian11"
    raulmysql.vm.hostname = "raulmysql"
    raulmysql.vm.network "private_network", ip: "192.168.10.20",
              virtualbox__intnet: "redmysql"
    raulmysql.vm.network "public_network"
    raulmysql.vm.provision "shell", path: "scriptmysql.sh"
  end
end
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

