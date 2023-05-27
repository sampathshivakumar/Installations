## Step by Step guide to install Apache Tomcat on Amazon Linux ##
![10](https://user-images.githubusercontent.com/119833411/241388181-f7114c28-8bd7-4b06-8911-4cb483b7a469.jpg)
### Prerequisites:
* Amazon Linux Machine with a minimum of 1GB RAM. It will be sufficent to do A proof of concept (POC).
* Open Port.No: 8080 in EC2-security group.
### Install Java.
```
sudo su - 
amazon-linux-extras install java-openjdk11=latest -y

```
version of java to be installed dependes up on tomcat version: https://tomcat.apache.org/whichversion.html
### Download Tomcat Binary file.
tomcat-10 download page: https://tomcat.apache.org/download-10.cgi
```
# Become a root
sudo su -
cd /opt
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.9/bin/apache-tomcat-10.1.9.tar.gz
# unzip tomcat binary
tar -xvzf apache-tomcat-10.1.9 
# Rename for simplicity 
mv apache-tomcat-10.1.9 tomcat
```
### Create a tomcat user.
its not a good practice to run tomcat using root user.
```
# Become a root,no need to execute this cmd if your already root user.
sudo su -
# create a tomcat user
adduser tomcat
# create a password for tomcat user
passwd tomcat 
# enter the New password then Retype new password, you should see passwd: all authentication tokens updated successfully.
```
### Now change the ownership of /opt/tomcat file from root to tomcat being a root user.
```
# Become a root, no need to execute this cmd if your already root user.
sudo su - 
chown -R tomcat:tomcat /opt/tomcat
```
![11](https://user-images.githubusercontent.com/119833411/241390867-eaff65ca-b903-4a1f-8011-0b90ead9213e.jpg)
### Now switch to tomcat user and make following changes.
```
su - tomcat
cd /opt/tomcat
# Create a tomcat user and assign manager-gui, manager-script ,manager-jmx, manager-status roles.
vi conf/tomcat-users.xml
# Add the below line before tomcat-users-tag.
<user username="sampath" password="sampath" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
</tomcat-users>
press Esc
:wq 
```
![12](https://user-images.githubusercontent.com/119833411/241391537-6601999f-5c4d-4bfc-a3b7-d759cd2a4397.jpg)
```
# enter the below command in tomcat directory.
find . -name context.xml
# you will see the following lines.
./conf/context.xml
./webapps/docs/META-INF/context.xml
./webapps/examples/META-INF/context.xml
./webapps/host-manager/META-INF/context.xml
./webapps/manager/META-INF/context.xml
#comment value tag sections in below all files
vi ./webapps/examples/META-INF/context.xml
vi ./webapps/host-manager/META-INF/context.xml
vi ./webapps/manager/META-INF/context.xml
```
![14](https://user-images.githubusercontent.com/119833411/241392098-2ef70cfd-4645-4f7c-b60c-141f78454358.jpg)
### In tomcat-10 Execute Permission are already present to catalina.sh, startup.sh & shutdown.sh
if your going with tomcat-9 or others give execute Permission.
```
# Go to bin directory.
cd /opt/tomcat/bin
chmod +x catalina.sh startup.sh  shutdown.sh
```
### Create a link files for Tomcat Server up and Down.
```
ln -s /opt/apache-tomcat-9.0.55/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/apache-tomcat-9.0.55/bin/shutdown.sh /usr/local/bin/tomcatdown
# Now start the tomcat. 
tomcatup
```
### Now access the tomcat by web-browser.
open a new tab and enter
http://Public IPv4 address:8080/

### you should see tomcat page.
![15](https://user-images.githubusercontent.com/119833411/241392947-688e9545-db12-4f3e-8c57-e97e40520a50.jpg)

### You can access Server Status, Manager App and Host Manager by entering tomcat username and password.
```
# if you have changed it use what you have used in tomcat-users.xml file.
username="sampath" 
password="sampath"

```

### Hope this post was helpful for you all. please leave feedback at sampathshivakumar@gmail.com , https://www.linkedin.com/in/sampathsivakumar-boddeti-1666b810b/ if any thankyou.