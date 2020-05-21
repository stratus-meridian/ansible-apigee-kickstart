Vagrant.configure("2") do |config|
  config.vm.box = "centos/8"

  config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true

  config.vm.provision "ansible" do |ansible|
    ansible.playbook           = "playbook.yml"
    ansible.compatibility_mode = "2.0"
    ansible.inventory_path     = "inventory.ini"
    ansible.limit              = "vagrant"
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 1
  end
end
