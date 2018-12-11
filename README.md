# Jenkins-CI-CD-Pipeline-Maven

Included Technologies: EC2, Maven, Jenkins

Languages: Java

This project demonstrates the process to configure a Jenkins continuous integration server on Amazon EC2. Once configured, Jenkins will be set up to build a Java projet with Maven, pulling the project from GitHub automatically, each time a change is pushed to a GitHub repository. Also, line coverage reports will be generated on project unit tests using junit and jacoco plugins.

Project summary can be found here: www.mikiasemanuel.com/jenkins-ci-cd-pipeline-maven

## Prerequisites:

Jenkins Administrative Server Build is outlined [here](https://github.com/MikiasE/Jenkins-CI-CD-Pipeline-Maven/tree/master/Jenkins%20Administrative%20Server%20Build).

Tomcat Web Application Server Build is outlined [here](https://github.com/MikiasE/Jenkins-CI-CD-Pipeline-Maven/tree/master/Tomcat%20Web%20Server%20Build).

Install Recommended Jenkins Plugins.

Install "Maven Invoker" Jenkins Plugin.

Specify JDK and Maven Path in Jenkins Global Tool Configuration.
