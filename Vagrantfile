#Criação de Arquivo Vagrant .nginx
#v1.0
Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.provision "shell", path: "provision.sh"
  config.vm.network "public_network", bridge: "wlp2s0"
  #config.vm.network "forwarded_port", guest: 80, host: 8086
end