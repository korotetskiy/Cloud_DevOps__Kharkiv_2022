Configuration Management. Ansible 
===============

1. Installing Ansible
Add the following line to /etc/apt/sources.list:

    > deb http://ppa.launchpad.net/ansible/ansible/ubuntu [version Linux Name] main
        
    Then run these commands:

    > $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
    > $ sudo apt-get update
    > $ sudo apt-get install ansible
    > $ cd /etc/ansible/

hosts - server config file
ansible.cfg - Ansible config file


> $ sudo mkdir playbooks

Playbook creations:
   
 >   $ cd playbooks/
 >    nano install_mc.yml
    
  
>    - [**git reflog**  commands output](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/task1.1_GIT.txt) 

>    - [*my experience with a GIT*](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/myExperienceWithGIT.txt)

>    - [*Describe in your own words what DevOps is*](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/DevOps.txt)

### REPORT IN SCREENSHOT
> 1.	Install GIT on your workstation. 
> 2.	Setup git: change your global configs (add name and email, setup core text editor). 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/1.jpg)

> 3. Create account on GitHub. 
> 4. Create new private repo on GitHub. 
Repo name: DevOps_online_<City>_<year><quarter> Example: DevOps_online_Dnipro_2021Q4

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/2.jpg)

> 6. Clone repo to your workstation.

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/3.jpg)

> 7. Open git console in root directory of your project and make next steps. 
> 8. Do all your experiments in folder “task1.1”. 
> 9. Create empty readme.txt file. 
> 10. Make init commit. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/4.jpg)

> 11. Create develop branch and checkout on it. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/5.jpg)

> 12. Create index.html empty file. Commit. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/6.jpg)

> 13. Create branch with name “images”. Checkout on it. Add images folder with some images inside it. Commit. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/7.jpg)

> 14. Change your index.html. Add images source inside it. Commit. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/8.jpg)















