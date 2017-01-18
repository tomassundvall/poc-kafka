# -*- mode: ruby -*-
# vi: set ft=ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "hyperv" do |v, override|
    override.vm.box = "maxx/ubuntu16"
  end
end
