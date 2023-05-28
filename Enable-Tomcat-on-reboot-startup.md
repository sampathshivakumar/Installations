## How to Start Tomcat Automaticaly At The Startup and Reboot of The Instance.
![10](https://user-images.githubusercontent.com/119833411/241497546-e611cc72-d4ba-478e-8977-579266835886.jpg)

### Observation.
**If you have installed Tomcat By downloading Binaryfile,Then you might have observed that Tomcat will not start after stop and start or reboot of your server.**

### Execute the following commands to Enable-Tomcat on reboot and startup of your instance.
```
# Become a root user.
sudo su -

# Download java.
amazon-linux-extras install java-openjdk11=latest -y

# Check java version
java --version 

# Change directory to opt.
cd /opt

# Download the tomcat binary file.
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.9/bin/apache-tomcat-10.1.9.tar.gz 

# Extract the file.
tar -xvzf apache-tomcat-10.1.9.tar.gz

# Rename the file. 
mv apache-tomcat-10.1.9 tomcat

# Change directory to /etc/init.d 
cd /etc/init.d

# Create a file name tomcat.
vi tomcat

# Past the below content.
--------------------------------------------------------------------------------------------------------------------------------
#!/bin/bash
# description: Tomcat Start Stop Restart  
# process-name: tomcat  
# chkconfig: 234 20 80
CATALINA_HOME=/opt/tomcat
case $1 in  
start)  
sh $CATALINA_HOME/bin/startup.sh  
;;   
stop)     
sh $CATALINA_HOME/bin/shutdown.sh  
;;   
restart)  
sh $CATALINA_HOME/bin/shutdown.sh  
sh $CATALINA_HOME/bin/startup.sh  
;;   
esac      
exit 0 
-------------------------------------------------------------------------------------------------------------------------------

# Now give Execute permissions to tomcat file.
chmod +x tomcat

#  Adds the "tomcat" service to the system's startup configuration.
chkconfig --add tomcat

# Configuring the "tomcat" service to start automatically at runlevels 2, 3, and 4.
chkconfig --level 234 tomcat on

# Start the tomcat.
service tomcat start

#Sets the "tomcat" service to start automatically when the system boots up.
chkconfig tomcat on

```

### You Have Successfully Enabled Tomcat on reboot and startup of your instance.

### Note:-
* **In this Post i have focused on only Enabling The Tomcat on reboot and startup of your instance.** 
* **Creation of tomcat users and assigning roles to them and some best practices were discussed in my previous post.**
* **You can check it here. https://gist.github.com/sampathshivakumar/d46e0bd855648cdaaba68a87c75a10cc**

### Thank you for reading this post! I hope you found it helpful. If you have any feedback or questions, please feel free to reach out to me at sampathshivakumar@gmail.com or connect with me on LinkedIn at https://www.linkedin.com/in/sampathsivakumar-boddeti-1666b810b/. Your feedback is valuable to me. Thank you!
 

