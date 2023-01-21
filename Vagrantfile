# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.ssh.guest_port = 22

  config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/bionic64"
    master.vm.network "public_network", ip: "172.20.0.11", bridge: "vlan0001"
  end

  config.vm.define "worker" do |worker|
    worker.vm.box = "ubuntu/bionic64"
    worker.vm.network "public_network", ip: "172.20.0.12", bridge: "vlan0001"
  end

  config.vm.define "worker1" do |worker1|
    worker1.vm.box = "ubuntu/bionic64"
    worker1.vm.network "public_network", ip: "172.20.0.13", bridge: "vlan0001"
  end

  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("/home/victor/.ssh/id_ed25519.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /home/ubuntu/.ssh/authorized_keys
    SHELL
  end

end
