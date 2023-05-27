## Step by Step guide to install Jenkins on Amazon Linux.
![1](https://user-images.githubusercontent.com/119833411/241403167-c18c66fb-7b35-4c87-9bc5-ec7bd403062d.jpg)
### Prerequisites:
**Minimum hardware requirements:**
* 256 MB of RAM Enough for doing proof of concept (POC). 
* 1 GB of drive space (although 10 GB is a recommended minimum if running Jenkins as a Docker container)
**Recommended hardware configuration for a small team:**
* 4 GB+ of RAM.
* 50 GB+ of drive space.
**Software requirements:**
* Jenkins require Java-11 or later versions.
* Open Port.No 8080 in EC2-security group. (8080 is Default port of Jenkins)
### Launch an Amazon Linux EC2 instance.
* instance-type: t2.micro 
### Download Jenkins.
Go to Jenkins Download page:-https://www.jenkins.io/download/

**Select LTS** 
![2](https://user-images.githubusercontent.com/119833411/241405049-445e50d6-8e15-42b3-9de7-899fa903b338.jpg)

**Select Red Hat/Fedora/Alma/Rocky/CentOS**
![3](https://user-images.githubusercontent.com/119833411/241405139-8bf4fff6-7b4a-45b0-8066-4a09645b00ea.jpg)
**You will see following command**
![4](https://user-images.githubusercontent.com/119833411/241405814-3f643c95-1cc1-4c60-adf2-0a2cac019b7e.jpg)

### Connect to instance and execute following commands. 
```
# Become a root
sudo su -

# Jenkins repo is added to yum.repos.d
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

# Import key from Jenkins
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# Install Java-11
amazon-linux-extras install java-openjdk11 -y

# Install Jenkins
yum install jenkins -y
```

### Start Jenkins.
```
# Become a root, no need to execute if you are alread root.
sudo su -

# You can enable the Jenkins service to start at boot with the command:
systemctl enable jenkins

# You can start the Jenkins service with the command:
systemctl start jenkins

# You can check the status of the Jenkins service using the command:
systemctl status jenkins
```

### Open Web-Browser and access jenkins on port 8080.
```
http://<Public-IPv4-address>:8080/
```
### You should see the following page.
![5](https://user-images.githubusercontent.com/119833411/241408010-caf9ff80-dcc9-4c64-aa23-0241db676689.jpg)

```
cat /var/lib/jenkins/secrets/initialAdminPassword
# you will get the password.
```
![6](https://user-images.githubusercontent.com/119833411/241408673-70f1a2bc-7792-4936-84c6-34f894cc8e5e.jpg)

**Copy the Password and past in Web-Browser then press continue.**

![7](https://user-images.githubusercontent.com/119833411/241408735-fff1bd5c-6a39-483a-80e8-70a9085af78b.jpg)

**Go with Install Suggested Plugins.**
![8](https://user-images.githubusercontent.com/119833411/241409217-49994812-ded3-4dcd-be1c-aa7a47478c64.jpg)

**Suggested Plugins will start downloading.**
![9](https://user-images.githubusercontent.com/119833411/241409495-d0ddb512-9384-4735-8d0b-530f07e229de.jpg)

**Fill the details and click save and continue.**
![10](https://user-images.githubusercontent.com/119833411/241409915-064e078d-35c0-486e-afa0-e7c068ec7fb9.jpg)

**Click on Save and Finish.**
![11](https://user-images.githubusercontent.com/119833411/241410580-e8630d51-e21e-4cd4-a078-45b7ae57f21a.jpg)

**Jenkins is ready click on start using Jenkins**
![12](https://user-images.githubusercontent.com/119833411/241410588-70a0b2fe-7807-4a9b-84e1-8fa1eba101a9.jpg)

**Jenkins is successfully installed**
![13](https://user-images.githubusercontent.com/119833411/241410684-376c06df-ca86-4b54-a5cd-4c22f6075cbc.jpg)

### Thank you for reading this post! I hope you found it helpful. If you have any feedback or questions, please feel free to reach out to me at sampathshivakumar@gmail.com or connect with me on LinkedIn at https://www.linkedin.com/in/sampathsivakumar-boddeti-1666b810b/. Your feedback is valuable to me. Thank you!
