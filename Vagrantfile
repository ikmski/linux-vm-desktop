Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "4096"
    vb.customize [
      "modifyvm", :id,
      "--vram", "256",
      "--clipboard", "bidirectional",
      "--draganddrop", "bidirectional",
      "--cpus", "2",
      "--ioapic", "on"
    ]
  end

  config.vm.provision "shell", inline: "
    apt-get update -y
    DEBIAN_FRONTEND=noninteractive apt-get install -y ansible
"

  config.vm.provision "ansible_local" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provision/site.yml"
    ansible.inventory_path = "provision/inventory"
    ansible.limit = "ubuntu"
  end

end
