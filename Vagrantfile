
N = 2

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.define "Kube-master" do |master|
    master.vm.network "private_network", ip: "192.168.10.105"
    master.vm.hostname = "Kube-master"
    master.vm.synced_folder "./Playbooks", "/home/ubuntu/Playbooks"
    master.vm.synced_folder "./Dockerfiles", "/home/ubuntu/Dockerfiles"
    master.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/home/ubuntu/Playbooks/master_playbook.yml"
      ansible.extra_vars = {
        node_ip: "192.168.10.105"
      }
    end
  end

  (1..N).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.box = "ubuntu/xenial64"
      node.vm.network "private_network", ip: "192.168.10.#{105 + i}"
      node.vm.hostname = "node-#{i}"
      node.vm.synced_folder "./Playbooks", "/home/ubuntu/Playbooks"
      node.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "/home/ubuntu/Playbooks/node_playbook.yml"
        ansible.extra_vars = {
          node_ip: "192.168.10.#{105 + i}"
        }
      end
    end
  end
end
