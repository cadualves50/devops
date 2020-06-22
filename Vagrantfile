#Scripr de passagem via shell
$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql -e "create user 'phpuser'@'%' identified by 'pass';"
SCRIPT

#Criação de Arquivo Vagrant .so Padrão
#v1.0
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "public_network"

#Criação de máquina Ngnix
config.vm.define "ngnix" do |ngnix|
  ngnix.vm.provision "shell", path: "provision.sh"
  ngnix.vm.network "public_network", ip: "192.168.0.23"
  ngnix.vm.network "forwarded_port", guest: 80, host: 8086
  end
#Criação de máquina Mysql

config.vm.define "mysqldb" do |mysql|
  mysql.vm.network "public_network", ip: "192.168.0.24"
  mysql.vm.provision "shell", inline: $script_mysql
   mysql.vm.provision "shell",
     inline: "cat /configs/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf"
   mysql.vm.provision "shell", inline: "service mysql restart"
   mysql.vm.synced_folder "./configs", "/configs"
   mysql.vm.synced_folder ".", "/vagrant", disabled: true
   end
#Criação de máquina Php

  config.vm.define "phpweb" do |phpweb|
  phpweb.vm.network "forwarded_port", guest: 8888, host: 8889
  phpweb.vm.network "public_network", ip: "192.168.0.25"
  phpweb.vm.provision "shell", inline: "apt-get update && apt-get install -y puppet"
  phpweb.vm.provision "puppet" do |puppet|
    puppet.manifests_path = "./configs/manifests"
    puppet.manifest_file = "phpweb.pp"
  end
  end

end