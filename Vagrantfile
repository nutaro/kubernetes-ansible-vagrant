IMAGE_NAME = "ubuntu/jammy64"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "forwarded_port", guest: 8001, host:  8001, auto_correct: true
        master.vm.network "forwarded_port", guest: 6433, host:  6433, auto_correct: true
        master.vm.network "forwarded_port", guest: 30002, host:  30002, auto_correct: true
        master.vm.network "private_network", ip: "192.168.56.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/master-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.56.10",
            }
        end
    end

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "forwarded_port", guest: 8001, host:  8001, auto_correct: true
            node.vm.network "forwarded_port", guest: 6433, host:  6433, auto_correct: true
            node.vm.network "forwarded_port", guest: 30002, host:  30002, auto_correct: true
            node.vm.network "private_network", ip: "192.168.56.1#{i}"
            node.vm.hostname = "node-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/node-playbook.yml"
                ansible.extra_vars = {
                    node_ip: "192.168.56.1#{i}",
                }
            end
        end
    end
end
