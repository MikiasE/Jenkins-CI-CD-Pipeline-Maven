# Installation and Configuration of Jenkins Administrator Server w/ Proxy

## Prerequisites:
```
Create EC2 Instance - (Jenkins Server) (Ubuntu Server 18.04 LTS (HVM), SSD Volume Type – ami-0ac019f4fcb7cb7e6 | t2.micro)
If using proxy: Create Security Group and open SSH, HTTP, HTTPS ports.
If not using proxy: Create Security Group with SSH and Custom TCP connection on localhost port 8080 (also open on ufw).
Run commands as root (add sudo prefix for non-root)
```
### Install Apache and Proxy
```
apt-get install apache2 -y
a2enmod proxy
a2enmod proxy_http
```
### Configure Server to allow SSH and HTTP Access
```
apt-get update
ufw allow 'OpenSSH'
ufw allow 'Apache'
ufw enable
y
```
### Install Java8, Maven, and Git
```
add-apt-repository ppa:webupd8team/java
apt-get update
apt-get install oracle-java8-installer maven git-core -y
apt-get install language-pack-en -y
```
### Set Java Environmental Variables
```
apt-get install oracle-java8-set-default
```
### Install Jenkins
```
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | apt-key add -
sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
apt-get update
apt-get install jenkins -y
```
### Configure and Start Apache2 Proxy
```
vim /etc/apache2/sites-available/jenkins.conf

<VirtualHost *:80>
	ServerName [INSERT YOUR PUBLIC DNS]
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
*now the application can run with the public DNS*
