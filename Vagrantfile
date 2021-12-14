Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        echo "192.168.1.230  master-node" >> /etc/hosts
        echo "192.168.1.231  worker-node01" >> /etc/hosts
        echo "192.168.1.232  worker-node02" >> /etc/hosts
    SHELL
    
    config.vm.define "master" do |master|
      master.vm.box = "bento/ubuntu-20.10"
      master.vm.hostname = "master-node"
      master.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)", ip: "192.168.1.230"
      master.vm.provider "virtualbox" do |vb|
          vb.memory = 4048
          vb.cpus = 2
      end
      master.vm.provision "shell", path: "scripts/common.sh"
      master.vm.provision "shell", path: "scripts/master.sh"
    end

    (1..2).each do |i|
  
    config.vm.define "node0#{i}" do |node|
      node.vm.box = "bento/ubuntu-20.10"
      node.vm.hostname = "worker-node0#{i}"
      node.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)", ip: "192.168.1.23#{i}"
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 1
      end
      node.vm.provision "shell", path: "scripts/common.sh"
      node.vm.provision "shell", path: "scripts/node.sh"
    end
    
    end
  end