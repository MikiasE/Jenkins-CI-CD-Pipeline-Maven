# Installation and Configuration of Tomcat Web Server (8.5)

## Prerequisites:
```
Create EC2 Instance - (Tomcat Web Server) (Amazon Linux 2 AMI (HVM), SSD Volume Type - ami-009d6802948d06e52 | t2.micro)
Create Security Group and open SSH and TCP Custom "8090" ports.
Run commands as root (add sudo prefix for non-root)
```
### Install Java
```
yum install java-1.8* -y
```
### Install, Configure, and Start Tomcat
```
yum install wget -y
cd /opt/
wget https://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.tar.gz
tar -zvxk apache-tomcat-8.5.35.tar.gz
cd /apache-tomcat-8.5.25/bin/
chmod +x startup.sh
chmod +x shutdown.sh
./startup.sh
```
### Edit Connector Port
```
# this is edited to avoid conflict with Jenkins connector port which is 8080. (I am assuming no proxy for my Web Server).
cd /opt/apache-tomcat-8.5.35/conf/
vi server.xml

# Change connector port setting to "8090" ( <Connector port="8090" protocol="HTTP/1.1")
cd /opt/apache-tomcat-8.5.35/bin/

# Restart service
./shudown.sh
./startup.sh
```
### Edit manager/html (to access outside of local browser)
```
cd /opt/apache-tomcat-8.5.35/webapps/host-manager/META-INF
vi context.xml

# comment out line: <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
[ESC]:wq 
cd /opt/apache-tomcat-8.5.35/webapps/manager/META-INF
vi context.xml

# same process at last line
[ESC]:wq
cd /opt/apache-tomcat-8.5.35/bin/

# Restart service
./shudown.sh
./startup.sh
```
### Create Users
```
/opt/apache-tomcat-8.5.35/conf
vi tomcat-users.xml

# Customize users and remove comment indicators
  <role rolename="manager-gui"/>
  <role rolename="manager-sript"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <user username="admin" password="admin" roles="manager-gui, manager-sript, manager-jmx, manager-status"/>
  <user username="tomcat" password="s3cret" roles="manager-gui"/>
</tomcat-users>
[ESC]:wq
cd /opt/apache-tomcat-8.5.35/bin/

# Restart service
./shudown.sh
./startup.sh
```
