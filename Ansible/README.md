Configuration Management. Ansible 
===============

1. Installing Ansible on Ubuntu 20.04/22.04</br>
Add the following line to /etc/apt/sources.list:

    > deb http://ppa.launchpad.net/ansible/ansible/ubuntu [version Linux Name] main
        
    Then run these commands:

    > $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
    
    > $ sudo apt-get update
    
    > $ sudo apt install software-properties-common
    
    > $ sudo add-apt-repository --yes --update ppa:ansible/ansible
    
    > $ sudo apt-get install ansible
    
    > $ cd /etc/ansible/
   
   <img src="https://github.com/korotetskiy/img/blob/main/a_inst.jpg">

hosts - Servers config file</br>
ansible.cfg - Ansible config file


> $ sudo mkdir playbooks

Playbook creations:
   
 >   $ cd playbooks/
 >    nano install_mc.yml
    
  
