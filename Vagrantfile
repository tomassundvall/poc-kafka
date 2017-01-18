# -*- mode: ruby -*-
# vi: set ft=ruby
Vagrant.configure("2") do |config|
  # Configure the boxes
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "hyperv" do |v, override|
    override.vm.box = "maxx/ubuntu16"
  end

  config.vm.provision "shell", inline: "apt-get update -y && apt-get install python python-pip -y"
  #
  # Run Ansible from the Vagrant Host
  #
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "main.yaml"
  end
  config.vm.define 'n1' do |n|
    n.vm.hostname = 'n1'
    n.vm.network "private_network", ip: "172.20.20.10"
  end
  config.vm.define 'n2' do |n|
    n.vm.hostname = 'n2'
    n.vm.network "private_network", ip: "172.20.20.11"
  end
  config.vm.define 'n3' do |n|
    n.vm.hostname = 'n3'
    n.vm.network "private_network", ip: "172.20.20.12"
  end

  #
  ## this is our ansible controller VM which provisions the other VMs
  #i
  config.vm.define "controller" do |controller|
    controller.vm.network :private_network, ip: "192.168.33.15"
    controller.vm.hostname = "controller"
    # install ansible
    controller.vm.provision "shell", privileged: false, path: "install_ansible.sh"
    # run ansible
    controller.vm.provision "shell", privileged: false, inline: <<-EOF
        if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
          wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant -O /home/vagrant/.ssh/id_rsa
          wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/vagrant/.ssh/id_rsa.pub
          chmod 600 /home/vagrant/.ssh/id_*
        fi
        rm -rf /tmp/provisioning
        cp -r /vagrant/provisioning /tmp/provisioning
        cd /tmp/provisioning
        chmod -x hosts
        export ANSIBLE_HOST_KEY_CHECKING=False
        ansible-playbook playbook.yml --inventory-file=hosts
      EOF
    end
end
