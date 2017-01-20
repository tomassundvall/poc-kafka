# Kafka Proof of Concept repository

This readme walks you thorugh how to configure the setup using vagrant and
ansible.

    ansible-galaxy install --role-file=requirements.yml --roles-path=./roles
    vagrant up

## Creating a new role

    ansible-galaxy init role_name

## References

 - [Ansible docs][ansible-docs]
 - [Ansible Galaxy][ansible-galaxy]

## How to install and get HyperV running with Vagrant and Ubuntu 16.04

1. Enable HyperV from "Programs and Features" in Control panel
2. Create a virtual switch (internal) in Hyper-V manager
3. Download and install Vagrant
4. Use vagrant box called maxx/ubuntu16. If on internal net, the box can be
   added by running "vagrant box add maxx/ubuntu16 <path>"
5. When running vagrant up, specify provider using --provider=hyperv

## TODO

 - [ ] Ansible bootstrap for Ubuntu
   - [ ] Inventory file
 - [ ] The nodes
   - [x] 3 Zookeeper + Kafka
   - [ ] Schema registry
 - [ ] Roles
   - [ ] Kafka
     - [ ] Upgrade repo from `requirements.txt` to Ubuntu 16.04 (SystemD)
   - [ ] Zookeeper
     - [ ] Upgrade repo from `requirements.txt` to Ubuntu 16.04 (SystemD)
   - [ ] SSH
   - [ ] SSH Keys
   - [ ] apt
   - [x] apt security updates
   - [ ] auditd
   - [ ] ntpd

 [ansible-docs]: https://docs.ansible.com/
 [ansible-galaxy]: https://docs.ansible.com/ansible/galaxy.html
 
 ##Installing kafka via commandline (last line starts kafka)
 
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo wget http://apache.mirrors.spacedump.net/kafka/0.10.1.1/kafka_2.10-0.10.1.1.tgz
sudo apt-get install zookeeperd

sudo mkdir /opt/Kafka
cd /opt/Kafka
sudo tar -xvf kafka_2.10-0.10.1.1.tgz -C /opt/Kafka/
sudo  /opt/Kafka/kafka_2.10-0.10.1.1/bin/kafka-server-start.sh /opt/Kafka/kafka_2.10-0.10.1.1/config/server.properties
.

