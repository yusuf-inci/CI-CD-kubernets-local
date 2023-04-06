# Jenkins, Nexus and SonarQube Servers Environment with Vagrant

This project is an example for creating multi-machine environments with Vagrant. It includes a Vagrantfile that contains Jenkins, Nexus, and SonarQube servers.

## Prerequisites

Before running this Vagrantfile, you need to install the following tools on your machine:

- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)
- install vagrant-hostmanager and vagrant-vbguest plugin
 $ vagrant plugin install vagrant-hostmanager
 $ vagrant plugin install vagrant-vbguest

## Usage

1. Clone the repository: `git clone https://github.com/user/project.git`
2. Navigate to the project directory: `cd project`
3. Start the Vagrant virtual machine: `vagrant up` 
 - This will create the virtual machines for Jenkins, Nexus, and SonarQube servers with the necessary
software and configuration.
4. Connect to the virtual machines:
   - To connect to the Jenkins server: `vagrant ssh JenkinsServer`
   - To connect to the Nexus server: `vagrant ssh NexusServer`
   - To connect to the SonarQube server: `vagrant ssh SonarServer`

## Configuration
The Vagrantfile contains the following configuration:

- config.hostmanager.enabled = true: Enables the vagrant-hostmanager plugin, which automatically 
updates the hosts file on the host machine with the private network IP addresses of the virtual 
machines.
- config.hostmanager.manage_host = true: Automatically adds the virtual machine hostnames and IP 
addresses to the /etc/hosts file on the virtual machines themselves.
- config.vm.define: Defines each virtual machine with its own settings, such as the box, hostname, 
private IP address, memory, CPU, and provisioning script.

## Customizing the Vagrantfile

You can customize the Vagrantfile to your needs by modifying the following parameters:

- vb.memory: The amount of memory allocated to each virtual machine.
- vb.cpus: The number of CPUs allocated to each virtual machine.
- config.vm.network: The IP address and network settings for each virtual machine.
- create a custom script file and modify the `config.vm.provision` lines in the Vagrantfile.

## Vagrant Commands

Vagrant provides a set of useful commands for working with virtual machines. Here are some commonly used ones:

- `vagrant up`: Starts the virtual machine.
- `vagrant ssh`: Connects to the virtual machine via SSH.
- `vagrant halt`: Halts the virtual machine.
- `vagrant resume`: Resumes the halted virtual machine.
- `vagrant suspend`: Suspends the virtual machine.
- `vagrant destroy`: Destroys the virtual machine.
- `vagrant validate`: Validates the Vagrantfile.
- `vagrant plugin`: Manages Vagrant plugins.
- `vagrant provision`: Reprovisions the virtual machine.

For more Vagrant commands, please see the [Vagrant documentation](https://www.vagrantup.com/docs/cli).

## Contributing

To contribute to this project, please follow these steps:

- Fork the project.
- Create a new branch: git checkout -b my-branch-name.
- Make the changes you want and commit: git commit -m "Description".
- Submit your changes: git push origin my-branch-name.
- Create a new pull request and explain your changes.

## License

This project is licensed under the [MIT license](LICENSE).
