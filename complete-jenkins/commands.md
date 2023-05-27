# Complete Jenkins Tutorial | Learn Jenkins From Scratch In 3 Hours 
- url: https://www.youtube.com/watch?v=nCKxl7Q_20I 

## Install Jenkins With war File
- be sure jdk 8 or jdk 11 installed
`apt install openjdk-11-jre-headless`
- run following command inside the folder war file stand
`java -jar jenkins.war`
- get the initial password and log in jenkins server via browser. on this case
`http://192.168.56.11:8080`
- configure user and install suggested plugins

## Install and Configure Maven Plugin
- Dashboard ==> Manage Jenkins ==> Global Tool Configuration ==> Maven installations ==> name: Maven3 
==> save
- Dashboard￼==> Manage Jenkins￼==> Plugin Manager ==> available ==> Maven Integration plugin ==> install

## Integration jenkins with Github

1. Integration Pre-Requisite
- GitHub must be able to send data to Jenkins
- Jenkins must have a public IP 
- Except for on-premise GitHub instances 
