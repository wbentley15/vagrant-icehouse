# -*- mode: ruby -*-

# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
# Silly Ubuntu 12.04 doesn't have the
# --stdin option in the passwd utility
echo root:vagrant | chpasswd

cat << EOF >> /etc/hosts
192.168.236.40 infra1
192.168.236.50 infra2
192.168.236.60 infra3
192.168.236.70 compute2
EOF
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos-6.5-x86_64"

  # Turn off shared folders
  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

  # Begin infra1
  config.vm.define "infra1" do |infra1_config|
    infra1_config.vm.hostname = "infra1"

    infra1_config.vm.provision "shell", inline: $script

    # eth1
    infra1_config.vm.network "private_network", ip: "192.168.236.40"
    # eth2
    infra1_config.vm.network "private_network", ip: "192.168.240.40"
    
    infra1_config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = "1024"
        v.vmx["numvcpus"] = "1"
    end

    infra1_config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "1024"]
        v.customize ["modifyvm", :id, "--cpus", "1"]
        v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end
  # End infra1

  # Begin infra2
  config.vm.define "infra2" do |infra2_config|
    infra2_config.vm.hostname = "infra2"

    infra2_config.vm.provision "shell", inline: $script

    # eth1
    infra2_config.vm.network "private_network", ip: "192.168.236.50"
    # eth2
    infra2_config.vm.network "private_network", ip: "192.168.240.50"
        
    infra2_config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = "1024"
        v.vmx["numvcpus"] = "1"
    end

    infra2_config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "1024"]
        v.customize ["modifyvm", :id, "--cpus", "1"]
        v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end
  # End infra2
  
  # Begin infra3
  config.vm.define "infra3" do |infra3_config|
    infra3_config.vm.hostname = "infra3"

    infra3_config.vm.provision "shell", inline: $script

    # eth1
    infra3_config.vm.network "private_network", ip: "192.168.236.60"
    # eth2
    infra3_config.vm.network "private_network", ip: "192.168.240.60"
        
    infra3_config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = "1024"
        v.vmx["numvcpus"] = "1"
    end

    infra3_config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "1024"]
        v.customize ["modifyvm", :id, "--cpus", "1"]
        v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end
  # End infra3
 
  # Begin compute2
  config.vm.define "compute2" do |compute2_config|
    compute2_config.vm.hostname = "compute2"

    compute2_config.vm.provision "shell", inline: $script

    # eth1
    compute2_config.vm.network "private_network", ip: "192.168.236.70"
    # eth2
    compute2_config.vm.network "private_network", ip: "192.168.240.70"
    
    compute2_config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = "2048"
        v.vmx["numvcpus"] = "2"
    end

    compute2_config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "2048"]
        v.customize ["modifyvm", :id, "--cpus", "2"]
        v.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
    end
  end
  # End compute2
end