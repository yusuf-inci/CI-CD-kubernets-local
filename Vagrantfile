Vagrant.configure("2") do |config|
    config.hostmanager.enabled = true 
    config.hostmanager.manage_host = true

    # ### JenkinsServer VM  ####
    # config.vm.define "JenkinsServer" do |jenkins|
        # jenkins.vm.box = "ubuntu/focal64"
        # jenkins.vm.hostname = "JenkinsServer"
        # jenkins.vm.network "private_network", ip: "192.168.56.11"
        # jenkins.vm.provider "virtualbox" do |vb|
            # vb.memory = "2048"
            # vb.cpus = "2"
        # end
        # jenkins.vm.provision "shell", path: "userdata/jenkins.sh"
    # end

    ### NexusServer VM  ###
    config.vm.define "NexusServer" do |nexus|
        nexus.vm.box = "bento/amazonlinux-2"
        nexus.vm.hostname = "NexusServer"
        nexus.vm.network "private_network", ip: "192.168.56.21"
        nexus.vm.provider "virtualbox" do |vb|
            vb.memory = "4096"
            vb.cpus = "2"
        end
        #nexus.vm.synced_folder ".", "/vagrant", type: "nfs"
        nexus.vm.provision "shell", path: "userdata/nexus.sh"
    end


    ### NexusServer VM  ###


end
                                  