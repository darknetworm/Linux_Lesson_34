# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.define "server" do |server|
    server.vm.hostname = "server.loc"
    server.vm.network "private_network", ip: "192.168.56.10"
  end
  config.vm.define "client" do |client|
    client.vm.hostname = "client.loc"
    client.vm.network "private_network", ip: "192.168.56.20"
  end
  config.vm.provision "ansible" do |ansible|
#Для проверки различных типов vpn следует заменить Ansible файл
#tun.yml - для режима tun, tap.yml - для режима tap и ras.yml - для RAS с клиентскими сертификатами
    ansible.playbook = "ras.yml"
    ansible.inventory_path = "hosts"
  end
end
