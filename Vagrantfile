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
end
