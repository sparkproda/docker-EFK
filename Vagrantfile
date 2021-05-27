IMAGE_NAME = "bento/ubuntu-18.04"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 10240
        v.cpus = 2
    end

    config.vm.box_check_update = false

    config.vm.define "hostefk01" do |master|
        master.vm.box = IMAGE_NAME

        master.vm.network "private_network", ip: "192.168.88.11"
        master.vm.network "private_network", ip: "192.168.99.12", name: "vboxnet6"
        master.vm.hostname = "hostefk01"
        master.vm.provider :virtualbox do |v|
            v.customize ["modifyvm", :id, "--memory", 4096]
            v.customize ["modifyvm", :id, "--cpus", 2]
        end        
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "devcluster/efk01-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.88.11",
            }
        end
    end

    config.vm.define "hostefk02" do |slave|
        slave.vm.box = IMAGE_NAME

        slave.vm.network "private_network", ip: "192.168.88.12"
        slave.vm.network "private_network", ip: "192.168.99.13", name: "vboxnet6"
        slave.vm.hostname = "hostefk02"
        slave.vm.provider :virtualbox do |v|
            v.customize ["modifyvm", :id, "--memory", 4096]
            v.customize ["modifyvm", :id, "--cpus", 2]
        end        
        slave.vm.provision "ansible" do |ansible|
            ansible.playbook = "devcluster/efk02-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.88.12",
            }
        end
    end
    config.vm.define "hostefk03" do |slave|
        slave.vm.box = IMAGE_NAME

        slave.vm.network "private_network", ip: "192.168.88.13"
        slave.vm.network "private_network", ip: "192.168.99.14", name: "vboxnet6"
        slave.vm.hostname = "hostefk03"
        slave.vm.provider :virtualbox do |v|
            v.customize ["modifyvm", :id, "--memory", 4096]
            v.customize ["modifyvm", :id, "--cpus", 2]
        end        
        slave.vm.provision "ansible" do |ansible|
            ansible.playbook = "devcluster/efk03-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.88.13",
            }
        end
    end






end    