IMAGE_NAME = "ubuntu/jammy64"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "public_network", ip: "172.20.0.10", bridge: "vlan0001"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/master-playbook.yml"
            ansible.extra_vars = {
                node_ip: "172.20.0.10",
            }
        end
    end

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "public_network", ip: "172.20.0.1#{i}", bridge: "vlan0001"
            node.vm.hostname = "node-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/node-playbook.yml"
                ansible.extra_vars = {
                    node_ip: "172.20.0.1#{i}",
                }
            end
        end
    end
end
