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

2. Configuration files hosts and ansible.cfg </br>
hosts - Servers config file</br>
ansible.cfg - Ansible config file


> $ sudo mkdir playbooks

====================================
1. Ansible - что это и для чего? Разбираем основы
Если вы только установили Ansible, необходимо перейти в его каталог и проверить содержимое:

    # переходим
    cd /etc/ansible/
    # проверяем содержимое и права
    ls -la
    drwxr-xr-x   3 root root  4096 сен 18 12:22 .
    drwxr-xr-x 122 root root  4096 окт 10 15:03 ..
    -rw-r--r--   1 root root 20340 сен 15 13:58 ansible.cfg
    -rw-r--r--   1 root root   615 сен 18 12:22 hosts

Немного теории
Ansible - это система управления конфигурациями, написанная на Python. Более простым языком: это универсальный инструмент позволяющий выполнять некий структурированный список команд (написанный на языке YML, в виде скрипта) на нескольких серверах.
Если у вас несколько серверов 5...100, то при попытке даже простого обновления пакетов, вы потеряете уйму времени на подключение к каждому из этих серверов по отдельности. Ansible дает универсальное средство решить данную проблему, как? читаем дальше!

2. Настройка файла hosts под наши сервера
Прежде всего нам надо настроить список наших серверов, на которые мы будем отправлять наши данные. Для этого заходим в файл hosts:

    sudo nano hosts

Содержимое файла hosts будем примерно таким:

    # Ex 1: Ungrouped hosts, specify before any group headers.
     
    #green.example.com
    #192.168.0.8
     
    # Ex 2: A collection of hosts belonging to the 'webservers' group
     
    #[webservers]
    #alpha.example.org
    #192.168.1.100
    ...

Допустим у нас есть сервера c IP 192.168.0.10 и 192.168.0.20 (локальный). Добавим наши сервера в файл выше и укажем данные для подключения к ним (пояснения прямо в коде):

    ...
    # Ex 2: A collection of hosts belonging to the 'webservers' group
    ...
    [debi_servers]
    #можно просто указать сервер, его IP
    192.168.0.10
    #можно присвоить имя, указать пользователя и его пароль
    debi ansible_host=192.168.0.20 ansible_user=debiuser ansible_pass=password123
    ...

Пример заполнения выше, с данными пользователя, не совсем корректный. Лучше использовать SSH. О том как его настроить, ссылка на статью в самом начале. Смотрим где у нас находится ключ SSH:

    # из корня домашней папки переходим в папку с ключами
    cd .ssh
    # проверяем содержание
    ls -la
    итого 28
    drwx------  2 debuser debuser 4096 окт  9 16:34 .
    drwxr-xr-x 18 debuser debuser 4096 окт 10 15:02 ..
    -rw-------  1 debuser debuser  399 сен 11 12:02 id_ed25519
    -rw-r--r--  1 debuser debuser   95 сен 11 12:02 id_ed25519.pub
    # смотрим путь до ключа
    pwd
    /home/debuser/.ssh

Вносим эти данные в наш файл hosts:

    [debi_servers]
    #убрали один сервер и добавили ссылку на SSH ключ
    debi ansible_host=192.168.0.20 ansible_user=debiuser ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519

Можно попробывать подключиться к серверу. Есть один момент, при подключении первый раз к серверу он спросит отпечаток: "Are you sure you want to continue connecting (yes/no)". После подтверждения, он больше не спрашивает. Но если вы подключаетесь первый раз к 100 серверам, то придеться отвечать по каждому. Простая команда для примера:

    ansible -i hosts all -m ping
    The authenticity of ...
    ... Are you sure you want to continue connecting (yes/no)
    debi | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }

Чтобы отменить проверку отпечатка на каждый сервер и не прописывать файл сервера, заполняем файл ansible.cfg. Обычно эти значения уже есть в шаблоне, надо только их раскомментировать:

    [defaults]
    # строчка которая указывает файл с серверами по умолчанию
    inventory      = /etc/ansible/hosts
    # строчка которая отменяет проверку первичного подключения (yes/no)
    host_key_checking = false

Повторяем команду выше, но уже сокращенный вариант:

    # all - все сервера из файла, -m модуль
    ansible all -m ping
    debi | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }

3. Создаем файл inventory или hosts

Объединение серверов в группы:
Допустим у вас много серверов: сервера баз, сервера приложений, сервера итогового проекта PROD. Тогда это можно записать в файл hosts в разных вариантах:

    # все сервера ниже входят в группу all
     
    192.168.0.12
    192.168.0.14
     
    [debi_servers]
    debi ansible_host=192.168.0.20 ansible_user=debiuser ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519
    debi2 ansible_host=192.168.0.32 ansible_user=debiuser ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519
     
    # тестовый пред прод сервер баз
    [staging_DB]
    192.168.0.1
    192.168.0.2
     
    # тестовый пред прод сервер баз 2 (обратите внимание на индекс DB и db, это разные группы)
    [staging_db]
    192.168.0.3
    192.168.0.4
     
    # тестовый пред прод сервер приложений
    [staging_APP]
    192.168.0.5
    192.168.0.6
     
    # тестовый пред прод сервер приложений
    [prod_APP]
    192.168.0.7
    192.168.0.8
     
    # сервер базы PROD
    [prod_DB]
    192.168.0.15
    192.168.0.16
     
    # Объединим группы серверов в одну более крупную
    [staging_ALL:children]
    staging_DB
    staging_db
    staging_APP
     
    # группа которая объединяет все DB
    [DB_ALL:children]
    staging_DB
    staging_db
    prod_DB

Тем самым, вот так просто вы можем составлять группы, а в созданные группы еще группы. Это удобно, главное не переборщить.

Объединение общих данных для серверов:
Теперь объединим данные для авторизации для серверов debi:

Было:

    ...
    [debi_servers]
    debi ansible_host=192.168.0.20 ansible_user=debiuser ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519
    debi2 ansible_host=192.168.0.32 ansible_user=debiuser ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519
    ...

Стало:

    ...
    [debi_servers]
    debi ansible_host=192.168.0.20
    debi2 ansible_host=192.168.0.32
    ...
    # так как у нас одинаковые пользователи и ключи, переносим их в отдельный блок
    [debi_servers:vars]
    ansible_user=debiuser
    ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519
    ...

Свободные переменные для серверов:

    ...
    # Объединим группы серверов в одну более крупную
    [staging_ALL:children]
    staging_DB
    staging_db
    staging_APP
    ...
    # staging_ALL - группа выше, параметру message присвоили значение Help. Это значение можно применять в рамках всей нашей группы "staging_ALL"
    [staging_ALL:vars]
    message=Help
    ...


Просмотреть переменные, группы и сервера:

    # Фрагмент выполнения команды
    ansible-inventory --list
    {
        "_meta": {
            "hostvars": {
                "debi": {
                    "ansible_host": "192.168.0.20",
                    "ansible_ssh_private_key_file": "/home/debuser/.ssh/id_ed25519",
                    "ansible_user": "debiuser"
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
                "debi"
            ]
        },
        "ungrouped": {}
    }
    ...

Или в виде графа:

    # фрагмент
    ansible-inventory --graph
    @all:
      |--@test_server:
      |  |--debi
      |--@ungrouped:
    ...

4. Выносим общие переменные из файла hosts
В пункте 3 мы вынесли общие переменные с данными пользователя в отдельный блок. Но на практике, такие данные более професионально выносить в отдельный файл. Это мы сейчас и сделаем:

Было:

    ...
    [debi_servers]
    debi ansible_host=192.168.0.20
    debi2 ansible_host=192.168.0.32
    ...
    # так как у нас одинаковые пользователи и ключи, переносим их в отдельный блок
    [debi_servers:vars]
    ansible_user=debiuser
    ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519
    ...

Проверям что у нас в каталоге Ansible:

    ls -la
    drwxr-xr-x   3 root root  4096 окт 14 13:21 .
    drwxr-xr-x 122 root root  4096 окт 14 10:34 ..
    -rw-r--r--   1 root root 20340 сен 15 13:58 ansible.cfg
    -rw-r--r--   1 root root   670 окт 14 13:21 hosts

Создаем директорию group_vars и переходим в неё:

    sudo mkdir group_vars
    ls -la
    drwxr-xr-x   4 root root  4096 окт 14 14:07 .
    drwxr-xr-x 122 root root  4096 окт 14 10:34 ..
    -rw-r--r--   1 root root 20340 сен 15 13:58 ansible.cfg
    drwxr-xr-x   2 root root  4096 окт 14 14:07 group_vars
    -rw-r--r--   1 root root   670 окт 14 13:21 hosts
    cd group_vars

Создаем файл с нашим именем группы серверов debi_servers:

    nano debi_servers

Внутри прописываем:

    # знак "="меняем на ":", это важно!
    ansible_user                  :  debiuser
    ansible_ssh_private_key_file  :  /home/debuser/.ssh/id_ed25519
    # добавим данные: для какого сервера и имя автора
    environment                   :  PROD
    owner                         :  Kostya

Сохраняем. В файле hosts эти строчки полностью стираете:

    [debi_servers:vars]
    ansible_user=debiuser
    ansible_ssh_private_key_file=/home/debuser/.ssh/id_ed25519

=======================================================


Playbook creations:
   
 >   $ cd playbooks/
 >    nano install_mc.yml
    
  
