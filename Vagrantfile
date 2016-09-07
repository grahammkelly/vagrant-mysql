# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_API_VER = "2"
VM_NAME = "mysql-test-server"
Vagrant.configure(VAGRANT_API_VER) do |config|
  config.vm.hostname = VM_NAME
  config.vm.box = "psysdev/basebox-ubuntu-14.04-java8-mysql"

  # config.vm.network "forwarded_port", guest: 3306, host: 3306
  config.vm.network "private_network", ip: "192.168.33.15"

  config.vm.synced_folder "#{Dir.pwd}/data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    # vb.cpus = 2
    vb.name = VM_NAME
  end

  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo "Ensuring the English locale is available"
      sudo locale-gen en_IE.UTF-8

      # Create the SSH keys to allow direct SSH onto the box (not through vagrant)
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
  end
end
