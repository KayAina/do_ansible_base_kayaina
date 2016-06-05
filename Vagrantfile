Vagrant.configure("2") do |config|

config.vm.define :mgmt do |mgmt_config|
    mgmt_config.vm.box = "ubuntu/trusty64"
    mgmt_config.vm.hostname = "mgmt"
    mgmt_config.vm.network :private_network, ip: "10.0.15.10"
    mgmt_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
    end 
    mgmt_config.vm.provision :shell, path: "bootstrap-mgmt.sh"
end

config.vm.define :lb do |lb_config|
    lb_config.vm.box = "ubuntu/trusty64"
    lb_config.vm.hostname = "lb"
    lb_config.vm.network :private_network, ip: "10.0.15.11"
    lb_config.vm.network "forwarded_port", guest: 80, host: 1250
    lb_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
    end                                  
end

(1..2).each do |i|
 config.vm.define "web#{i}" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.hostname = "web#{i}"
    node.vm.network :private_network, ip: "10.0.15.2#{i}"
    node.vm.network "forwarded_port", guest: 80, host: "125#{i}"
    node.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
    end                                  
 end
end

end