Setting up Datadog 101

My Enviornment:
- OS: Ubuntu 16.04
- VM: Vagrant w/ VirtualBox

Set yourself up for success:
- Download Vagrant: https://www.vagrantup.com/
- Download VirtualBox: https://www.virtualbox.org/
- Install Homebrew through your terminal: https://brew.sh/ (I DONT THINK THIS IS NEEDED)

Create a directory to work in

	$ mkdir [HOSTNAME]
	
cd into that directory

	$ cd into [HOSTNAME]
	
Start up vagrant

	$ vagrant init ubuntu/trusty64	
- This will create your Vagrantfile
    - More info on ubuntu/trusty64: https://app.vagrantup.com/ubuntu/boxes/trusty64
    
In your text editor, [HOSTNAME]/Vagrantfile:
(Copy & Paste this code)

	Vagrant.configure("2") do |config|
	 config.vm.box = "ubuntu/trusty64"
	 config.vm.provider "virtualbox" do |vb|
	   vb.memory = 2048
	   vb.cpus = 4
	 end
	  
	 config.vm.network "private_network", ip: "192.168.33.10"
	 
	 config.vm.synced_folder ".", "/var/www/html", :nfs => { :mount_options => ["dmode=777", "fmode=666"] }
	 
	 config.vm.provision "shell", path: "bootstrap.sh"

	 end
- Save the file

Create a new file in your directory: [HOSTNAME]/bootstrap.sh
(Copy & Paste this code)


	apt-get update
	apt-get upgrade
	apt-get install -y git
	apt-get install -y apache2
	a2enmod rewrite
	apt-add-repository ppa:ondrej/php
	apt-get update
	apt-get install -y php7.2
	apt-get install -y libapache2-mod-php7.2
	service apache2 restart
	apt-get install -y php7.2-common
	apt-get install -y php7.2-mcrypt
	apt-get install -y php7.2-zip
	debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
	debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
	apt-get install -y mysql-server
	apt-get install -y php7.2-mysql
	sudo service apache2 restart
	
- Save the file
 
 Open VirtualBox:
 - VirtualBox can be found in Applications or recent downloads

Back to the terminal:

   	$ vagrant up
- You should see your directory in VirtualBox start up. 

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/VirtualBox_Running.png)

- SSH (Secure Shell) into a running Vagrant machine which will give you access to a shell.

     	$ vagrant ssh


Install Datadog Agent
*Add Photo




*Adding tags. 

	$ cd /etc/datadog-agent

	*Add PHOTO
	
Zookeeper Metrics

Since the project runs a basic Apache server let's integrate Apache Zookeeper into the project. 

	

*Add github photo of apache zookeeper

	cd into /etc/datadog-agent/conf.d/zk.d
	sudo nano zk.yaml
	
	
* Add terminal file
	


