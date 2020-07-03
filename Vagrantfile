#Arquivo de configuração VM

Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/trusty64"

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
    end

    config.vm.define "wordpress" do |m|
        m.vm.network "public_network", ip: "192.168.0.20"
    end

    config.vm.define "mysql" do |mysql|
        mysql.vm.network "public_network", ip: "192.168.0.21"
    end
end
