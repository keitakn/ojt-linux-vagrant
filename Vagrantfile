# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.box = "mvbcoding/awslinux"
  config.vm.boot_timeout = 120
  config.vm.network "private_network", ip: "192.168.33.100"
  config.vm.provider "virtualbox" do |vm|
    vm.customize ["modifyvm", :id, "--memory", "1024", "--cpus", "2", "--ioapic", "on", "--cableconnected1", "on"]
  end

  # 同階層に設置してある関連リポジトリを共有ディレクトリとしてマウント
  %w(
    ojt-node
  ).each do |dir|
    config.vm.synced_folder "../#{dir}", "/home/vagrant/#{dir}" if  File.exist?("../#{dir}")
  end

  config.vm.provision "network-restart", type: "shell", run: "always", inline: "sudo service network restart"
end
