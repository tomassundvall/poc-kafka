# Kafka Proof of Concept repository

## TODO

 - [ ] Vagrantfile that works in both VirtualBox and HyperV
 - [ ] Ansible bootstrap for Ubuntu
   - [ ] Inventory file
 - [ ] The nodes
   - [ ] 3 Zookeeper + Kafka
   - [ ] Schema registry
 - [ ] Roles
   - [ ] Kafka
   - [ ] Zookeeper
   - [ ] Op5/Consul
   - [ ] SSH
   - [ ] SSH Keys
   - [ ] apt
   - [ ] apt security updates
   - [ ] auditd
   - [ ] ntpd

## How to install and get HyperV running with Vagrant and Ubuntu 16.04

1. Enable HyperV from "Programs and Features" in Control panel
2. Create a virtual switch (internal) in Hyper-V manager
3. Download and install Vagrant
4. Use vagrant box called maxx/ubuntu16.
  4a. If on internal net, the box can be added by running "vagrant box add maxx/ubuntu16 <path>"
5. When running vagrant up, specify provider using --provider=hyperv
