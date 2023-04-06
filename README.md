Vagrantfile for Jenkins, Nexus and SonarQube Servers
This repository contains a Vagrantfile that sets up virtual machines for Jenkins, Nexus, and SonarQube servers.

Prerequisites
Before using this Vagrantfile, you will need to have the following installed on your machine:

Vagrant
VirtualBox
Installation
To install, simply clone this repository and run the following command in your terminal:

￼Copy code
vagrant up
This will create the virtual machines for Jenkins, Nexus, and SonarQube servers with the necessary software and configuration.

Configuration
The Vagrantfile contains the following configuration:

config.hostmanager.enabled = true: Enables the vagrant-hostmanager plugin, which automatically updates the hosts file on the host machine with the private network IP addresses of the virtual machines.
config.hostmanager.manage_host = true: Automatically adds the virtual machine hostnames and IP addresses to the /etc/hosts file on the virtual machines themselves.
config.vm.define: Defines each virtual machine with its own settings, such as the box, hostname, private IP address, memory, CPU, and provisioning script.
Usage
To access the virtual machines, you can use the following commands:

vagrant ssh JenkinsServer: SSH into the Jenkins server.
vagrant ssh NexusServer: SSH into the Nexus server.
vagrant ssh SonarServer: SSH into the SonarQube server.
You can also access the web interfaces of each server by opening the following URLs in your web browser:

Jenkins: http://192.168.56.11:8080/
Nexus: http://192.168.56.21:8081/
SonarQube: http://192.168.56.31:9000/
Contributing
Contributions are welcome! If you find a bug or have an idea for a new feature, please [describe how to contribute, such as creating a pull request].

License
This project is licensed under the [license name] License - see the LICENSE file for details.

Acknowledgments
[Optional: list any acknowledgments, such as inspirations or references used in the project].