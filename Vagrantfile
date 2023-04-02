Vagrant.configure("2") do |config|
    config.hostmanager.enabled = true 
    config.hostmanager.manage_host = true

### JenkinsServer VM  ####
    config.vm.define "JenkinsServer" do |JenkinsServer|
        JenkinsServer.vm.box = "ubuntu/focal64"
        JenkinsServer.vm.hostname = "JenkinsServer"
        JenkinsServer.vm.network "private_network", ip: "192.168.56.11"
        JenkinsServer.vm.provider "virtualbox" do |vb|
            vb.memory = "2048"
            vb.cpus = "2"
        end
        JenkinsServer.vm.provision "shell", path: "jenkins.sh"
    end

