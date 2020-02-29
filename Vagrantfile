Vagrant.configure("2") do |config|

  config.vbguest.auto_update = false


 config.vm.define "appserver" do |appserver|
    appserver.vm.box = "bento/centos-7.3"
    appserver.vm.network "private_network", ip: "172.28.128.4"
  end


  config.vm.define "appDeployer" do |appDeployer|
    appDeployer.vm.box = "bento/centos-7.3"
    appDeployer.vm.network "private_network", ip: "172.28.128.3"
    appDeployer.vm.provision "shell", inline: "sudo wget -P /tmp https://packages.chef.io/files/stable/inspec/4.18.97/el/7/inspec-4.18.97-1.el7.x86_64.rpm"
    appDeployer.vm.provision "shell", inline: "sudo yum -y install epel-release"
    appDeployer.vm.provision "shell", inline: "sudo yum -y install ansible"
    appDeployer.vm.provision "shell", inline: "sudo yum -y install git"
    appDeployer.vm.provision "shell", inline: "ssh-keygen -f id_rsa -t rsa -N ''"
    appDeployer.vm.provision "shell", inline: "cp -p id_rsa* .ssh"
    appDeployer.vm.provision "shell", inline: "sudo chown vagrant .ssh/id_rsa*"
    appDeployer.vm.provision "shell", inline: "sudo chgrp vagrant .ssh/id_rsa*"
    appDeployer.vm.provision "shell", inline: "sudo echo 172.28.128.4>>/etc/ansible/hosts"
    appDeployer.vm.provision "shell", inline: "echo vagrant >vagrant.password.file"
    appDeployer.vm.provision "shell", inline: "ssh-keyscan 172.28.128.4 >>.ssh/known_hosts"
    appDeployer.vm.provision "shell", inline: "sshpass -v -f vagrant.password.file ssh-copy-id -i .ssh/id_rsa.pub  -o StrictHostKeyChecking=no vagrant@172.28.128.4" 
    appDeployer.vm.provision "shell", inline: "sudo mkdir /home/vagrant/cis"
    appDeployer.vm.provision "shell", inline: "sudo cp /vagrant/hosts /home/vagrant/cis"
    appDeployer.vm.provision "shell", inline: "sudo cp /vagrant/requirements.yml /home/vagrant/cis"
    appDeployer.vm.provision "shell", inline: "sudo cp /vagrant/secure_build.yml /home/vagrant/cis"
    appDeployer.vm.provision "shell", inline: "sudo ansible-galaxy install -p /home/vagrant/cis/roles -r /home/vagrant/cis/requirements.yml" 
  end


end


