VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.provider :virtualbox do |v|
    v.name = "dev"
  end
  
  config.vm.box = "chef/centos-6.5"
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.synced_folder ".", "/var/www/html", type: "nfs"

  #
  # Provisioning by Ansible
  #
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/playbook.yml"
    ansible.inventory_path = "provision/inventories/hosts"
    ansible.limit = "all"
    ansible.extra_vars = {
      private_interface: "192.168.33.10",
      hostname: "dev"
    }
  end
end
