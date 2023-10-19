# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.require_version ">= 2.4.0"

Vagrant.configure("2") do |config|
    config.vm.define "Master" do |master|
      master.vm.box = "dummy"
    #   master.vm.network "private_network", type: "dhcp"
      master.vm.provider :aws do |aws, override|
        aws.access_key_id = "YOUR_ACCESS_KEY_ID"
        aws.secret_access_key = "YOUR_SECRET_ACCESS_KEY"
        aws.region = "us-west-2"
        aws.instance_type = "t2.micro"
        aws.ami = "ami-0c55b159cbfafe1f0" # Ubuntu 20.04 LTS AMI ID
        aws.subnet_id = "YOUR_SUBNET_ID" # Replace with your subnet ID
        aws.security_groups = ["YOUR_SECURITY_GROUP"] # Replace with your security group
        aws.keypair_name = "YOUR_KEYPAIR_NAME" # Replace with your keypair name
        aws.tags = {
          Name: "Master"
        }
      end
  
      master.ssh.username = "ec2-user"
      master.ssh.private_key_path = "C:\\Users\\{the_path}\\{to_your_public_key}\\VagrantBoxes\\aws\\Vagrant.pem"
    end
  
    config.vm.define "Slave" do |slave|
      slave.vm.box = "dummy"
      slave.vm.provider :aws do |aws, override|
        aws.access_key_id = "YOUR_ACCESS_KEY_ID"
        aws.secret_access_key = "YOUR_SECRET_ACCESS_KEY"
        aws.region = "us-west-2"
        aws.instance_type = "t2.micro"
        aws.ami = "ami-0c55b159cbfafe1f0" # Ubuntu 20.04 LTS AMI ID
        aws.subnet_id = "YOUR_SUBNET_ID" # Replace with your subnet ID
        aws.security_groups = ["YOUR_SECURITY_GROUP"] # Replace with your security group
        aws.keypair_name = "YOUR_KEYPAIR_NAME" # Replace with your keypair name
        aws.tags = {
          Name: "Slave"
        }
      end
    end
  
    # Conditional synced folder based on OS
    if Vagrant::Util::Platform.windows? && system('rsync --version')
      config.vm.synced_folder '.', '/vagrant'
    else
      config.vm.synced_folder '.', '/vagrant', disabled: true
    end
  
    # Provisioning for both servers
    config.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y apache2 mysql-server php
      git clone https://github.com/laravel/laravel /var/www/html/laravel
      # Additional configuration steps for LAMP stack and Laravel application
    SHELL
  end
  