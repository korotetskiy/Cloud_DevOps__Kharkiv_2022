Configuration Management. Ansible 
===============

1. Installing Ansible on Ubuntu 20.04/22.04</br>
Add the following line to /etc/apt/sources.list:

```  
deb http://ppa.launchpad.net/ansible/ansible/ubuntu [version Linux Name] main
```
Then run these commands:

 ```
 $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
 $ sudo apt-get update
 $ sudo apt install software-properties-common
 $ sudo add-apt-repository --yes --update ppa:ansible/ansible
 $ sudo apt-get install ansible
 $ cd /etc/ansible/
 ```
   
   <img src="https://github.com/korotetskiy/img/blob/main/a_inst.jpg">

2. Configuration files hosts and ansible.cfg </br>
hosts - Servers config file</br>
ansible.cfg - Ansible config file

Change to the ansible directory and check the contents:

    
    $ cd /etc/ansible/
    $ ls -la
    drwxr-xr-x   3 root root  4096 Nov 18 12:22 .
    drwxr-xr-x 122 root root  4096 Nov 10 15:03 ..
    -rw-r--r--   1 root root 20340 Nov 15 13:58 ansible.cfg
    -rw-r--r--   1 root root   615 Nov 18 12:22 hosts

2.1 Setting up the hosts file for our servers

    $ sudo nano hosts

The contents of the hosts file will be something like this:

    # Ex 1: Ungrouped hosts, specify before any group headers.
     
    #green.example.com
    #192.168.0.8
     
    # Ex 2: A collection of hosts belonging to the 'webservers' group
     
    #[webservers]
    #alpha.example.org
    #192.168.1.100
    ...

We have servers with IP 192.168.0.10 and 192.168.0.20 (local). Let's add our servers to the file above and specify the data to connect to them:

    ...
    # Ex 2: A collection of hosts belonging to the 'webservers' group
    ...
    [test_servers]
    # IP
    192.168.0.10
    #you can assign a name, specify a user and his password
    test ansible_host=192.168.0.20 ansible_user=vkor ansible_pass=P@ssw0rd
    ...

 It's better to use an SSH key:

    # from the root of the home folder go to the folder with the keys
    cd .ssh
    # checking content
    ls -la
    total 28
    drwx------  2 vkor vkor 4096 Nov  9 16:34 .
    drwxr-xr-x 18 vkor vkor 4096 Nov 10 15:02 ..
    -rw-------  1 vkor vkor  399 Nov 11 12:02 id_ed25519
    -rw-r--r--  1 vkor vkor   95 Nov 11 12:02 id_ed25519.pub
    # look at the way to the key
    pwd
    /home/vkor/.ssh

We enter this data into our hosts file:

    [test_servers]
    #removed one server and added a link to the SSH key
    test ansible_host=192.168.0.20 ansible_user=vkor ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519

Now we try to connect to the server, the first time you connect to the server it will ask for a fingerprint: 

> "Are you sure you want to continue connecting (yes/no)". 

A simple example command:
>    ansible -i hosts all -m ping

The authenticity of ... Are you sure you want to continue connecting (yes/no)
    
    
  ```
  debi | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
```

To cancel the fingerprint check for each server and not prescribe the server file, fill in the ansible.cfg file. Usually these values are already in the template, you just need to uncomment them:

    [defaults]
    # a line that specifies a file with default servers
    inventory      = /etc/ansible/hosts
    #  line that cancels the primary connection check (yes/no)
    host_key_checking = false

We repeat the command above, but already an abbreviated version:

    # all - all servers from file, -m modul
    ansible all -m ping
    debi | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }

2.2 Create an inventory or hosts file

Combining servers into groups:
Let's say you have a lot of servers: a database server, an application server, a PROD final project server. Then it can be written to the hosts file in different ways:

    # servers below are in the all group
     
    192.168.0.12
    192.168.0.14
     
    [test_servers]
    test ansible_host=192.168.0.20 ansible_user=vkor ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
    test2 ansible_host=192.168.0.32 ansible_user=vkor ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
     
    # test pre-prod database server
    [staging_DB]
    192.168.0.1
    192.168.0.2
     
    # test pre-prod database server 2
    [staging_db]
    192.168.0.3
    192.168.0.4
     
    # test start pre-prod application server
    [staging_APP]
    192.168.0.5
    192.168.0.6
     
    # test pre-prod application server
    [prod_APP]
    192.168.0.7
    192.168.0.8
     
    # PROD database server
    [prod_DB]
    192.168.0.15
    192.168.0.16
     
    # Combine groups of servers into one larger one
    [staging_ALL:children]
    staging_DB
    staging_db
    staging_APP
     
    # A group that unites all DBs
    [DB_ALL:children]
    staging_DB
    staging_db
    prod_DB

Now let's combine authorization data for debi servers:
Fare:

    ...
    [test_servers]
    test ansible_host=192.168.0.20 ansible_user=vkor ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
    test2 ansible_host=192.168.0.32 ansible_user=vkor ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
    ...

It became:

    ...
    [test_servers]
    test ansible_host=192.168.0.20
    test2 ansible_host=192.168.0.32
    ...
    # since we have the same users and keys, we transfer them to a separate block
    [test_servers:vars]
    ansible_user=vkor
    ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
    ...

Free variables for servers:

    ...
    # combine groups of servers into one larger one
    [staging_ALL:children]
    staging_DB
    staging_db
    staging_APP
    ...
    # staging_ALL - group above, the message parameter was set to Help.
    [staging_ALL:vars]
    message=Help
    ...


View variables, groups and servers:

    # Command execution fragment
    ansible-inventory --list
    {
        "_meta": {
            "hostvars": {
                "test": {
                    "ansible_host": "192.168.0.20",
                    "ansible_ssh_private_key_file": "/home/vkor/.ssh/id_ed25519",
                    "ansible_user": "vkor"
                }
            }
        },
        "all": {
            "children": [
                "test_server",
                "ungrouped"
            ]
        },
        "test_server": {
            "hosts": [
                "test"
            ]
        },
        "ungrouped": {}
    }
    ...

Or as a graph:

    # fragment
    ansible-inventory --graph
    @all:
      |--@test_server:
      |  |--test
      |--@ungrouped:
    ...

2.3 Removing shared variables from the hosts file

Above, we moved the common variables with user data into a separate block. But in practice, it is more professional to transfer such data to a separate file. 
    ...
    [test_servers]
    testi ansible_host=192.168.0.20
    test2 ansible_host=192.168.0.32
    ...
    # ince we have the same users and keys, we transfer them to a separate block
    [debi_servers:vars]
    ansible_user=vkor
    ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
    ...

Let's check what we have in the ansible directory:

    ls -la
    drwxr-xr-x   3 root root  4096 Nov 14 13:21 .
    drwxr-xr-x 122 root root  4096 Nov 14 10:34 ..
    -rw-r--r--   1 root root 20340 Nov 15 13:58 ansible.cfg
    -rw-r--r--   1 root root   670 Nov 14 13:21 hosts

Create a group_vars directory and go to it:

    sudo mkdir group_vars
    ls -la
    drwxr-xr-x   4 root root  4096 Nov 14 14:07 .
    drwxr-xr-x 122 root root  4096 Nov 14 10:34 ..
    -rw-r--r--   1 root root 20340 Nov 15 13:58 ansible.cfg
    drwxr-xr-x   2 root root  4096 Nov 14 14:07 group_vars
    -rw-r--r--   1 root root   670 Nov 14 13:21 hosts
    cd group_vars

2.4 Create a file with server group names test_servers:

    nano test_servers

Inside we write:

    # the sign "=" is changed to ":", this is important!
    ansible_user                  :  vkor
    ansible_ssh_private_key_file  :  /home/vkor/.ssh/id_ed25519
    # add data: for which server and the name of the author
    environment                   :  PROD
    owner                         :  Vladimir

Save changes. In the hosts file, we completely erase these lines:

    [test_servers:vars]
    ansible_user=vkor
    ansible_ssh_private_key_file=/home/vkor/.ssh/id_ed25519
    
2.5 Checking Ansible inventory file
```
$ ansible-inventory --list -y
Output
all:
  children:
    servers:
      hosts:
        server1:
          ansible_host: 192.168.0.1
          ansible_python_interpreter: /usr/bin/python3
        server2:
          ansible_host: 192.168.0.2
          ansible_python_interpreter: /usr/bin/python3
        server3:
          ansible_host: 192.168.0.3
          ansible_python_interpreter: /usr/bin/python3
          ...
    ungrouped: {}
   
   ````
2.6 Connectivity testing Ansible hosts

```
$ ansible all -m ping -u root
Output
server1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
server2 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
server3 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

```

 3 Ansible Playbook creations</br>
 Let's, create a playbook:
 
 ```
 $ sudo nano /etc/ansible/example_playbook.yaml
 ```
 <img src="https://github.com/korotetskiy/img/blob/main/a_p1.png">
 
 Now we execute this Ansible playbook
 
 ```
 $ ansible-playbook /etc/ansible/example_playbook.yaml -K
 ```
<img src="https://github.com/korotetskiy/img/blob/main/a_p2.png">
 

 vkor@jsrv:~$ ansible-playbook my-first-playbook.yml --syntax-check

   
 >   $ cd playbooks/
 >    nano install_mc.yml
    
  Ansible is a configuration management system, a universal tool that allows you to execute a structured list of commands (written in YML, in the form of a script) on multiple servers.
