<h1>Part 1</h1>

<h2>Setting up Datadog 101</h2>

My Enviornment:
- OS: Ubuntu 16.04
- VM: Vagrant w/ VirtualBox

Ubuntu Setup with Agent
-----------------------
1. Set yourself up for success
- Download Vagrant: https://www.vagrantup.com/
- Download VirtualBox: https://www.virtualbox.org/
- Signup for a Datadog account: https://www.datadoghq.com/ (There is a free two week trial) 


2. Create a directory to work in

		$ mkdir [HOSTNAME]
	
3. cd into that directory

		$ cd into [HOSTNAME]
	
4. Start up vagrant

		$ vagrant init ubuntu/trusty64	
  This will create your Vagrantfile
    - More info on ubuntu/trusty64: https://app.vagrantup.com/ubuntu/boxes/trusty64
    
5. Copy the code to [HOSTNAME]/Vagrantfile and place within your text editor

		#COPY AND PASTE THIS CODE INTO YOUR FILE
		
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
			 
	*Optional: Feel free to setup your Vagrantfile however you please*

 6. Save the file

 7. Create a new file in your directory [HOSTNAME]/bootstrap.sh

		#COPY AND PASTE THIS CODE INTO YOUR FILE
		
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
		apt-get install -y mysql-server
		apt-get install -y php7.2-mysql
		sudo service apache2 restart

8. Save the file
 
9. Open VirtualBox

 - VirtualBox can be found in Applications or recent downloads

Back to the terminal:

10. Configure the Vagrantfile

 		$ vagrant up
		
- You should see your directory in VirtualBox start up. 

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/VirtualBox_Running.png)

11. SSH (Secure Shell) into a running Vagrant machine which will give you access to a shell

 		$ vagrant ssh





Installing Datadog Agent
------------------------

<p align="center">
<h4>Finally it's time! </h4>
</p>

![](https://i.imgur.com/KLxQESW.gif)


1. Copy & Paste the DD_API_KEY into your terminal


![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/Datadog_Ubuntu_Install.png)

- It should look someting like this...

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/9c73283a27966899fd81ab8d36dbc8c1cbfa3bc2/pictures/Datadog_Agent_Package.png)

<h4>That's it! You've officially installed Datadog</h4>
<br />


<br />

<h2>Adding Tags</h2> 
<a href="https://docs.datadoghq.com/tagging/#defining-tags">Datadog Tags</a>

*Although tags will not be used in this project, it is a very important part of Datadog*

- *Without the ability to assign and filter based on tags, finding problems in your environment and narrowing them down enough to discover the true causes could be difficult.*


In Your Terminal:

1. cd into the appropriate file

		$ cd /etc/datadog-agent
		
2. Edit datadog-agent.yaml using nano

		$ sudo nano datadog-agent.yaml

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/sudo_nano_datadog.png)

3. Once you're in the file, scroll down to tags

- *Remember to remove the "#"*

(See photo below for example)
![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/Datadog_workingTags.png)

4. Add desired tags

5. When the tags are in place, exit. 

6. Restart the Datadog agent
	
		$ sudo service datadog-agent restart
		
7. In the Datadog UI > Infrastructure > Host map > click on your host
- tags appear on the bottom right
		
![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/UI_Datadog_tags.png)
	
<h2> Using Integrations </h2>

<h4> Zookeeper Metrics </h4>

Since the project runs a basic Apache server let's integrate Apache Zookeeper into the project. 

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/Zookeeper_Integration.png)

1. cd into the appropriate file

		$ cd into /etc/datadog-agent/conf.d/zk.d
		
2. Edit the file using nano

		$ sudo nano zk.yaml
	
3. Setup your zk.yaml file

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/Zookeeper_Configuration_Terminal.png)

4. Once the Zookeeper setup is complete, restart the Datadog agent
	
		$ sudo service datadog-agent restart
		
5. Check on the status of your Datadog agent

		$ sudo service datadog-agent status
		
	<h3> If everything has an "OK", then you're doing great! </h3>
	- If there is an "ERROR", check out this <a href="https://docs.datadoghq.com/integrations/zk/">link</a>

6. In the Datadog UI >  Infrastructure > Host Map > Click on your host
	- Notice that "zookeeper" is now visible on your host
	


![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/9c73283a27966899fd81ab8d36dbc8c1cbfa3bc2/pictures/Datadog_showTags.png)


7. Click "zookeeper" and check out the metrics it is bringing into Datadog

<br>
<br>


<h2> Now that Zookeeper is running, let's setup a monitor for it. </h2>

- Since we set a timeout in Zookeeper, let's build a monitor around that.


1. Go to Datadog UI > Monitors > New Monitor

2. Setup the monitor as shown

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/9c73283a27966899fd81ab8d36dbc8c1cbfa3bc2/pictures/Zookeeper_Metrics.png)

![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/Zookeeper_Email_Metrics.png)


- This monitor will send a warning when there are more than 2 timeouts and will send an alert when there are more than 5 timeouts.

3. Check notifications

	![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/zookeeper_timeout_email.png)
	
	
	- Event
	![alt text](https://github.com/Perchitti/Perchitti_Lauren_SolutionsEngineer_031019/blob/master/pictures/zookeeper_timeout_event.png)
