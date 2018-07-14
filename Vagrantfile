# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|
  config.vm.define  "web1" do |host|
    host.vm.box = "centos/7"
    host.vm.hostname = "web1.example.com"
    host.vm.network "private_network", ip: "192.168.49.10"
    host.vm.provision "shell", path: "strap_apache1"
    host.vm.network "forwarded_port", guest: 80, host: 9000 
    host.vm.network "forwarded_port", guest: 443, host: 4000 
  end

  config.vm.define  "web2" do |host|
    host.vm.box = "centos/7"
    host.vm.hostname = "web2.example.com"
    host.vm.network "private_network", ip: "192.168.49.11"
    host.vm.provision "shell", path: "strap_apache2"
    host.vm.network "forwarded_port", guest: 80, host: 9001 
    host.vm.network "forwarded_port", guest: 443, host: 4001 
  end
  config.vm.define  "haproxy" do |host|
    host.vm.box = "centos/7"
    host.vm.hostname = "load.example.com"
    host.vm.network "private_network", ip: "192.168.49.12"
    host.vm.provision "shell", path: "strap_proxy"
    host.vm.network "forwarded_port", guest: 80, host: 9002 
    host.vm.network "forwarded_port", guest: 443, host: 4002 
    host.vm.network "forwarded_port", guest: 8080, host: 9003 
    host.vm.provision :reload
  end
end
