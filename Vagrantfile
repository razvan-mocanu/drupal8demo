# -*- mode: ruby -*-
# vi: set ft=ruby :

required_plugins = %w( vagrant-vbguest vagrant-hostsupdater )
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}; vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network "private_network", ip: "192.168.10.23"

  config.vm.provider :virtualbox do |vb|
    vb.name = "drupal.lokal"
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.hostname = "drupal.lokal"
  config.hostsupdater.aliases = ["www.drupal.lokal"]

  config.vm.provision "shell", path: "provision.sh"

  config.vm.synced_folder ".", "/vagrant", type: "nfs"
end
