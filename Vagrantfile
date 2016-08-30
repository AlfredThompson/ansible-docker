# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.box = "velocity42/xenial64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    #vb.name = "vagrant-ansible-docker-image-builder"
  end

  config.vm.define :vagrant do | vagrant_config |
  end

  config.vm.hostname = "vagrant"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get install software-properties-common -y
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install ansible -y
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "./ansible/provision.yml"
    ansible.sudo = true
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    ansible.host_key_checking = false
  end

  config.vm.synced_folder "ansible", "/src/ansible"

  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo ansible-playbook -i localhost, /src/ansible/docker-image-build.yml --extra-vars "role_inside_container=foo created_image_name=dockeredfoo created_image_version_tag=0.0.1"
  #   sudo ansible-playbook -i localhost, /src/ansible/docker-image-build.yml --extra-vars "role_inside_container=bar created_image_name=bar created_image_version_tag=vBeta"
  # SHELL

  config.vm.provision "shell", inline: <<-SHELL
    sudo ansible-playbook /src/ansible/playbook.yml -v
  SHELL

  #MultiVM things...
  #Incomplete
  # config.vm.define :vagrantAnsibleDockerImageBuilder do | vagrantAnsibleDockerImageBuilder_config |
  #
  #   config.vm.provision "shell", inline: <<-SHELL
  #     ansible-playbook -i localhost, /src/ansible/docker-registry.yml
  #   SHELL
  #
  # end



end
