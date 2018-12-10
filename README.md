# Jenkins-CI-CD-Pipeline-Maven

Included Technologies: EC2, Maven, Jenkins

Languages: Java

This project demonstrates the process to configure a Jenkins continuous integration server on Amazon EC2. Once configured, Jenkins will be set up to build a Java projet with Maven, pulling the project from GitHub automatically, each time a change is pushed to a GitHub repository. Also, line coverage reports will be generated on project unit tests using junit and jacoco plugins.

Project summary can be found here: 

## Prerequisites:
```
Create EC2 Instance - (Jenkins Server) (Ubuntu Server 18.04 LTS (HVM), SSD Volume Type – ami-0ac019f4fcb7cb7e6 | t2.micro)
Run as root (add sudo prefix for non-root)
```

### Configure Server for SSH:
```
apt-get update
ufw allow 'OpenSSH'
ufw allow ‘Apache’
ufw enable
```

### Install Apache and Proxy:
```
apt-get install apache2 -y
a2enmod proxy
a2enmod proxy_http
```

### Install Java8, Maven, and Git:
```
add-apt-repository ppa:webupd8team/java
apt-get update
apt-get install oracle-java8-installer maven git-core -y
apt-get install language-pack-en -y
```

### Install Jenkins:
```
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
apt-get update
apt install jenkins -y
```

### Configure and Enable Apache Proxy:
```
vim /etc/apache2/sites-available/jenkins.conf

<VirtualHost *:80>
	ServerName ec2-34-204-7-137.compute-1.amazonaws.com
	ProxyRequests Off
	<Proxy *>
		Order deny,allow
		Allow from all
	</Proxy>
	ProxyPreserveHost on
	ProxyPass / http://localhost:8080/
</VirtualHost>

a2ensite jenkins
service apache2 reload
```
