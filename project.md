Datadog Agent - Ubuntu

My Enviornment:
- OS: Ubuntu 16.04
- VM: Vagrant w/ VirtualBox

Set yourself up for success:
Download Vagrant: https://www.vagrantup.com/
Download VirtualBox: https://www.virtualbox.org/
Install Homebrew through your terminal: https://brew.sh/

Create a directory to work in

	$ mkdir [HOSTNAME]
cd into that directory

	$ cd into [HOSTNAME]
Start up vagrant

	$ vagrant init ubuntu/trusty64
- This will also create your Vagrantfile
    - More info on ubuntu/trusty64: https://app.vagrantup.com/ubuntu/boxes/trusty64
    
In [HOSTNAME]/Vagrantfile:
(Copy & Paste this code)

	Vagrant.configure("2") do |config|
	   #Box settings
	 config.vm.box = "ubuntu/trusty64"
	   #Provider Settings
	 config.vm.provider "virtualbox" do |vb|
	   vb.memory = 2048
	   vb.cpus = 4
	 end

	 config.vm.network "private_network", ip: "192.168.33.10"

	 end
 
 
Open VirtualBox


   	$ vagrant up
- As this runs, you should see your directory in VirtualBox start up. 
		
     	$ vagrant ssh
- This will SSH (Secure Shell) into a running Vagrant machine and give you access to a shell.

     	$ sudo apt update

    	$ sudo apt install -y git

     	$ sudo apt install -y apache2
*Basic Apache server is now running 


*Adding tags. 





