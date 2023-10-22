Vagrant.configure("2") do |config|

  # Master Server
  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/focal64"
    master.vm.network "private_network", type: "static", ip: "192.168.56.5"
    master.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
      vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
      vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
      vb.name = "master"
      vb.memory = "2048"
      vb.cpus = 1
    end

    # Install Ansible on the master
    master.vm.provision "shell", inline: "sudo apt-get update"
    master.vm.provision "shell", inline: "sudo apt-get install -y ansible"

    # Switch to the vagrant user and generate SSH keys
    master.vm.provision "shell", inline: "su - vagrant -c 'ssh-keygen -t rsa -N \"\" -f ~/.ssh/ansible_id_rsa'"

    master.vm.provision "shell", inline: "echo 'This is the Master Server'"
  end

  # Slave Server
  config.vm.define "slave" do |slave|
    slave.vm.box = "ubuntu/focal64"
    slave.vm.network "private_network", type: "static", ip: "192.168.56.6"
    slave.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
      vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
      vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
      vb.name = "slave"
      vb.memory = "2048"
      vb.cpus = 1
    end
    slave.vm.provision "shell", inline: "echo 'This is the Slave Server'"
  end
end
