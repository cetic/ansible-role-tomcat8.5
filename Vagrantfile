# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  require 'yaml'
  current_dir    = File.dirname(File.expand_path(__FILE__))
  configs        = YAML.load_file("#{current_dir}/config.yml")
  vagrant_config = configs['configs']

  config.vm.synced_folder "./", "/vagrant", owner: "vagrant", mount_options: ["dmode=775,fmode=600"]
	
	#Tomcat VM
    config.vm.define "tomcat" do |tomcat|

        tomcat.vm.provider :virtualbox do |v|
            v.memory = vagrant_config['tomcat']['ram']
            v.cpus = vagrant_config['tomcat']['cpu']
            v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
            v.customize ["modifyvm", :id, "--ioapic", "on"]
         end

         tomcat.vm.box = vagrant_config['tomcat']['box']
         tomcat.vm.network "private_network", ip: vagrant_config['tomcat']['ip']
         tomcat.vm.network :forwarded_port, guest: 8080, host: 8080
         tomcat.vm.hostname = vagrant_config['tomcat']['hostname']
    end

    #Controler VM
    config.vm.define "controller" do |controller|
        controller.vm.hostname = vagrant_config['controller']['hostname']
        controller.vm.box = vagrant_config['controller']['box']

        controller.vm.provider :virtualbox do |v|
            v.memory = vagrant_config['controller']['ram']
            v.cpus = vagrant_config['controller']['cpu']
            v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
            v.customize ["modifyvm", :id, "--ioapic", "on"]
         end

        controller.vm.network :private_network, ip: vagrant_config['controller']['ip']

        controller.vm.provision "ansible_local" do |ansible|
          ansible.galaxy_role_file = "tests/requirements.yml"
          ansible.playbook = "tests/playbook.yml"
          ansible.verbose = true
          ansible.install = true
          ansible.limit = "all"
          ansible.provisioning_path = "/vagrant"
          ansible.inventory_path = "tests/hosts"
        end
      end
end
