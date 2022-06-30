VAGRANTFILE_API_VERSION = "2"
VAGRANT_USERNAME = "vagrant"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "archlinux/archlinux"
  config.vm.network "private_network", ip: "192.168.56.5"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "4096"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "./provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/hosts"
    ansible.limit = "all"
    ansible.extra_vars = {
      ssh_remote_user: VAGRANT_USERNAME
    }
  end

  config.ssh.forward_agent = true
end
