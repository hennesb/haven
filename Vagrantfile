Vagrant.configure("2") do |config|

  config.vbguest.auto_update = false


 config.vm.define "appserver" do |appserver|
    appserver.vm.box = "bento/centos-7.3"
    appserver.vm.network "private_network", ip: "172.28.128.4"
  end


  config.vm.define "appDeployer" do |appDeployer|
    appDeployer.vm.box = "bento/centos-7.3"
    appDeployer.vm.network "private_network", ip: "172.28.128.3"
    appDeployer.vm.provision "shell", inline: "sudo yum -y install epel-release"
    appDeployer.vm.provision "shell", inline: "sudo yum -y install ansible"
    appDeployer.vm.provision "shell", inline: "ssh-keygen -f id_rsa -t rsa -N ''"
    appDeployer.vm.provision "shell", inline: "cp -p id_rsa* .ssh"
    appDeployer.vm.provision "shell", inline: "sudo chown vagrant .ssh/id_rsa*"
    appDeployer.vm.provision "shell", inline: "sudo chgrp vagrant .ssh/id_rsa*"
    appDeployer.vm.provision "shell", inline: "sudo echo 172.28.128.4>>/etc/ansible/hosts"
    appDeployer.vm.provision "shell", inline: "echo vagrant >vagrant.password.file"
    appDeployer.vm.provision "shell", inline: "ssh-keyscan 172.28.128.4 >>.ssh/known_hosts"
    appDeployer.vm.provision "shell", inline: "sshpass -v -f vagrant.password.file ssh-copy-id -i .ssh/id_rsa.pub  -o StrictHostKeyChecking=no vagrant@172.28.128.4" 
  end


end


