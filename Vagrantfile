N=2
Vagrant.configure("2") do |config|
  (1..N).each do |machine_id|
    config.vm.box = "sbeliakou/centos"
    config.vm.define "machine#{machine_id}" do |machine|
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.56.#{14+machine_id}"
      machine.ssh.insert_key = false
      config.vm.provider "virtualbox" do |vb|
        vb.name = "machine#{machine_id}"
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "30"]
        vb.memory = "2048"
      end
      if machine_id == 1
        machine.vm.hostname = "master-node"
      end
      if machine_id == 2
        machine.vm.hostname = "worker-node"
      end
      if machine_id == N
        machine.vm.provision :ansible do |ansible|
        ansible.playbook = "provision.yml"
        ansible.inventory_path = "./inventory"
        ansible.limit = "all"
        end
      end
    end
  end
end

