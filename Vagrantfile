VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  guest_ip = "192.168.33.10"

  config.vm.box = "chef/centos-6.5"
  config.vm.network :private_network, ip: guest_ip
  config.vm.synced_folder ".", "/var/www/html", type: "nfs"

  #
  # Provisioning by Ansible
  #
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/playbook.yml"
    ansible.inventory_path = "provision/inventories/hosts"
    ansible.limit = "all"
    ansible.extra_vars = {
      private_interface: guest_ip,
      hostname: "dev"
    }
  end
end
