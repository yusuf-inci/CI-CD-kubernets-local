Vagrant.configure("2") do |config|
    config.hostmanager.enabled = true 
    config.hostmanager.manage_host = true

    ### JenkinsServer VM  ###
    config.vm.define "JenkinsServer" do |jenkins|
        jenkins.vm.box = "ubuntu/focal64"
        jenkins.vm.hostname = "JenkinsServer"
        jenkins.vm.network "private_network", ip: "192.168.56.11"
        jenkins.vm.provider "virtualbox" do |vb|
            vb.memory = "2048"
            vb.cpus = "2"
        end
        jenkins.vm.provision "shell", path: "userdata/jenkins.sh"
    end

    ### NexusServer VM  ###
    config.vm.define "NexusServer" do |nexus|
        nexus.vm.box = "bento/amazonlinux-2"
        nexus.vm.hostname = "NexusServer"
        nexus.vm.network "private_network", ip: "192.168.56.21"
        nexus.vm.provider "virtualbox" do |vb|
            vb.memory = "3072"
            vb.cpus = "3"
        end
        nexus.vm.provision "shell", path: "userdata/nexus.sh"
    end


    ### SonarServer VM  ###
    config.vm.define "SonarServer" do |sonar|
        sonar.vm.box = "ubuntu/bionic64"
        sonar.vm.hostname = "SonarServer"
        sonar.vm.network "private_network", ip: "192.168.56.31"
        sonar.vm.provider "virtualbox" do |vb|
            vb.memory = "3072"
            vb.cpus = "3"
        end
        sonar.vm.provision "shell", path: "userdata/sonar.sh"
    end

end
                                  