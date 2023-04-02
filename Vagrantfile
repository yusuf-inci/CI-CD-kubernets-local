Vagrant.configure("2") do |config|
    config.hostmanager.enabled = true 
    config.hostmanager.manage_host = true

### JenkinsServer VM  ####
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
end
                                  