# Vagrant

For simple development tasks, CommandBox provides an [embedded development server](https://rorylaitila.gitbooks.io/lucee/content/lucee_server.html) which is easy to get started, however it is not suitable for running production servers. If you want to develop locally with a full VM that mirrors your production environment, [Vagrant](https://www.vagrantup.com) is a useful tool for this. 

Vagrant simply wraps a [VirtualBox VM](https://www.virtualbox.org/wiki/Downloads) and provides easy to use networking and file synchronization between your development environment and the VM. It also provides hooks for scripting automated setups of your environment. 

##Sample Vagrant File

This vagrant file cane be used to configure a Lucee VM. This section does not go into the specific of using Vagrant, for that follow a [Vagrant Tutorial](https://www.vagrantup.com/docs/). This vagrant file below uses a CentOS 6 VM and is not security hardended, it is only intended for development pruposes. It installs Lucee, Apache and MySQL, which is a common configuration.

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "nrel/CentOS-6.5-x86_64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "../", "/var/www/"

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

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
	pwd
     #Install Apache Server
     sudo yum -y install httpd
	 
     #For development purposes, turn off the firewall
     service iptables save
	 service iptables stop
	 chkconfig iptables off
	 
     #Install MySQL Server
     yum -y install mysql-server
	 chkconfig --level 345 mysqld on
	 
     #Download Lucee. Change the URL to latest versions from http://lucee.org/downloads.html
     wget http://d8yjolse1mixx.cloudfront.net/downloader.cfm/id/143/file/lucee-4.5.2.018-pl0-linux-x64-installer.run
     
     #Make the installer executable
	 chmod 755 lucee-4.5.2.018-pl0-linux-x64-installer.run
     
     #Run the installer in unattended mode and set the admin password
	 ./lucee-4.5.2.018-pl0-linux-x64-installer.run --mode unattended --railopass 123456
     
     #Install Nano text editor
	 yum -y install nano
     
     #Backup the http conf because we are going to edit it
     cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bak
     
     #When running VMs, apache caching static files (js, css, images) that are servers over the network from the host OS. Turning off MMAP and SendFile stops this caching
     sed -i -e 's/#EnableMMAP off/EnableMMAP off/g' /etc/httpd/conf/httpd.conf
	 sed -i -e 's/#Enable Sendfile Off/Enable Sendfile Off/g' /etc/httpd/conf/httpd.conf
     
     #Add index.cfm to the directory index
	 sed -i -e 's/DirectoryIndex index.html index.html.var/DirectoryIndex index.html index.html.var index.cfm/g' /etc/httpd/conf/httpd.conf	 
  SHELL
end

```