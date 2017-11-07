# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.vm.box = "debian/stretch64"
  config.vm.network "forwarded_port", guest: 80, host: 1080 , host_ip: "0.0.0.0"
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.define 'testnode' do |node|
      node.vm.hostname = 'test-web-node'
#      config.vm.network "private_network", ip: "192.168.33.10"
      node.hostmanager.aliases = %w(test1.local test2.local test3.local)
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "main.yml"
    ansible.extra_vars = {
        client: '["test1", "test2", "test3"]'
    }
    ansible.verbose = "v"
  end
end
