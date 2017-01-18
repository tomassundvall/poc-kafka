# -*- mode: ruby -*-
# vi: set ft=ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "hyperv" do |v, override|
    override.vm.box = "maxx/ubuntu16"
  end
  
  config.vm.define 'n1' do |n1|
    n1.vm.hostname = 'n1'
    n1.vm.network "private_network", ip: "172.20.20.10"
  end
  config.vm.define 'n2' do |n2|
    n2.vm.hostname = 'n2'
    n2.vm.network "private_network", ip: "172.20.20.11"
  end
  config.vm.define 'n3' do |n3|
    n3.vm.hostname = 'n3'
    n3.vm.network "private_network", ip: "172.20.20.12"
  end

  #
  ## this is our ansible controller VM which provisions the other VMs
  #
  config.vm.define "controller" do |controller|
    controller.vm.network :private_network, ip: "172.20.20.99"
    controller.vm.hostname = "controller"
    # install ansible
    controller.vm.provision "shell", privileged: false, path: "install_ansible.sh"
    # run ansible
    controller.vm.provision "shell", privileged: false, inline: <<-EOF
        if [ ! -f /home/ubuntu/.ssh/id_rsa ]; then
          wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant -O /home/ubuntu/.ssh/id_rsa
          wget --no-check-certificate https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub -O /home/ubuntu/.ssh/id_rsa.pub
          chmod 600 /home/ubuntu/.ssh/id_*
        fi
        rm -rf /tmp/provisioning
        cp -r /vagrant/provisioning /tmp/provisioning
        cd /tmp/provisioning
        chmod -x hosts
        export ANSIBLE_HOST_KEY_CHECKING=False
        ansible-playbook main.yml --inventory-file=hosts
      EOF
    end
end
