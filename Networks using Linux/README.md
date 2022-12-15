Networks using Linux
===============
> Практична частина модуля Linux Networking  передбачає створення засобами Virtual Box мережі, що показаний на малюнку </br><img src="https://github.com/korotetskiy/img/blob/main/n1.png">
Host – це комп’ютер, на якому запущений Virtual Box;
Server_1  – Віртуальна машина, на якій розгорнуто ОС Linux. Int1 цієї машини в режимі «Мережевий міст» підключений до мережі Net1, тобто знаходиться в адресному просторі  домашньої  мережі.  IP-адреса  Int1  встановлюється  статично  відповідно  до адресного  простору,  наприклад  192.168.1.200/24.  
нтерфейси  Int2  та  Int3  відповідно підключено в режимі «Внутрішня мережа» до мереж Net2 та Net3.
Client_1 та Client_2 – Віртуальні машини, на яких розгорнуто ОС Linux.  
Інтерфейси  підключені  в  режимі «Внутрішня мережа» до мереж Net2, Net3 та Net4 як показано на рисунку
Адреса  мережі  Net2 –10.90.6.0/24,
Адреса мережі Net3 –10.10.90.0/24
Адреса мережі Net4 –172.16.6.0/24. 
1. На Server_1 налаштувати статичні адреси на всіх інтерфейсах.
2. На  Server_1  налаштувати  DHCP  сервіс,  який  буде  конфігурувати  адреси  Int1 Client_1 та Client_2
3. За  допомогою  команд  ping  та  traceroute перевірити  зв'язок  між  віртуальними машинами. 
Результат пояснити. 
4. На  віртуальному  інтерфейсу  lo Client_1 призначити дві ІР  адреси  за  таким правилом:  172.17.D+10.1/24 та 172.17.D+20.1/24.  Налаштувати  маршрутизацію таким чином, щоб трафік з Client_2 до 172.17.D+10.1 проходив через Server_1, а до 172.17.D+20.1через Net4. Для перевірки використати traceroute.
5.Розрахувати  спільну  адресу  та  маску  (summarizing) адрес  172.17.D+10.1та 172.17.D+20.1,  при  чому префіксмає  бути  максимально  можливим.  Видалити маршрути,  встановлені  на  попередньому  кроці  та  замінити  їх  об’єднаним маршрутом, якій має проходити через Server_1.
6.Налаштувати  SSH  сервіс  таким  чином,  щоб  Client_1  та  Client_2  могли підключатись до Server_1 та один до одного. 
 
7.Налаштуйте на Server_1 firewall таким чином:
•Дозволено підключатись через SSH з Client_1 та заборонено з Client_2
• Client_2 на 172.17.D+10.1 ping  проходив, а на 172.17.D+20.1 не проходив
8.Якщо в п.3 була налаштована маршрутизація для доступу Client_1 та Client_2 до мережі  Інтернет – видалити  відповідні  записи.  На Server_1 налаштувати NATсервіс таким чином, щоб з Client_1 та Client_2 проходив ping в мережу Інтернет

•  DHCP SERVER - 10.83.10.100/24
•  CLIENT 1 - 10.83.10.10/24
CLIENT 2 - 10.83.10.20/24



### REPORT IN SCREENSHOT
> 1.	Install GIT on your workstation. 
> 2.	Setup git: change your global configs (add name and email, setup core text editor). 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/1.jpg)

> 3. Create account on GitHub. 
> 4. Create new private repo on GitHub. 
Repo name: DevOps_online_<City>_<year><quarter> Example: DevOps_online_Dnipro_2021Q4
> 5. You can see example repository structure. 
  	/ 
       	 m1/ 
task1.1/ 
m2/ 
task2.1/
 task2.2/ 
… 
… 
m8/
 task8.1/ 
task8.2/ 
…

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

> 15. Go back to develop branch. 
> 16. Create branch with name “styles”. Checkout on it. Add styles folder with styles source inside it. Commit. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/9.jpg)

> 17. Change your index.html. Commit. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/10.jpg)

> 18. Go to develop branch. 
> 19. Merge two new branches into develop using git merge command. Resolve conflict if it appear. Do it in next sequence: 
•merge “images” into “develop” 
•merge “styles” into “develop”
> 20. Do not delete any branches! 
> 21. Merge develop into master. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/11.jpg)

> 22. Try to inspect your repository with git log command. Use different options with this command (git log --help). 	
> 23. Push all your changes with all your branches to origin (git push origin --all). 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/12.jpg)

> 24. Execute command “git reflog“ and save it content somewhere (not in repository) with filename “task1.1_GIT.txt”. 

[![*Report in screenshots*](screenshot/1.png?raw=true)](https://github.com/vasilkyiv/DevOps_online_Kiev_2021Q4/tree/main/m1/task1.1/screenshot/13.jpg)

очистить существующие NAT правила:
	
iptables -t nat --flush


включить поддержку пересылки пакетов в /etc/sysctl.conf, чтобы трафик мог ходить между разными сетевыми интерфейсами.
Проверим текущее состояние:

sysctl -w net.ipv4.conf.all.forwarding=1

Чтобы после перезапуска системы оно не сбросилось, откроем файл /etc/sysctl.conf 
nano /etc/sysctl.conf
	
net.ipv4.conf.all.forwarding=1

iptables добавить правило, например:
iptables -t nat -A POSTROUTING -s 192.168.99.0/24 -j SNAT --to-source 172.16.16.94

Где, 192.168.99.0/24 внутренняя сеть, а 172.16.16.94 адрес через который нужно идти в интернет, аналогично прописываются другие внутренние сети.
Напомню маску для частных сетей:
	
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16

Если IP адрес на внешнем сетевом интерфейсе меняется (динамический), тогда вместо SNAT укажем MASQUERADE:
1
	
iptables -t nat -A POSTROUTING -s 192.168.99.0/24 -j MASQUERADE


post-up /sbin/iptables -t nat -A POSTROUTING -s 192.168.99.0/24 -o eth3 -j SNAT --to-source 172.16.90.1-172.16.90.5 --persistent


1. На Server_1 налаштувати статичні адреси на всіх інтерфейсах.
Int1  

Int2

Int3


2. На Server_1 налаштувати DHCP сервіс, який буде конфігурувати адреси Int1
Client_1 та Client_2

Edit file - nano /etc/default/isc-dhcp-server 

INTERFACES="eth1",  "eth2" - to Client_1 and Client_2  can get ip adress from DHCP

Instaling DHCP server

sudo apt install isc-dhcp-server

# minimal sample /etc/dhcp/dhcpd.conf
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.1.0 netmask 255.255.255.0 {
 range 192.168.1.150 192.168.1.200;
 option routers 192.168.1.254;
 option domain-name-servers 192.168.1.1, 192.168.1.2;
 option domain-name "mydomain.example";
}

3. За допомогою команд ping та traceroute перевірити зв'язок між віртуальними
машинами. Результат пояснити.




4. На віртуальному інтерфейсу lo Client_1 призначити дві ІР адреси за таким
правилом: 172.17.D+10.1/24 та 172.17.D+20.1/24. Налаштувати маршрутизацію
таким чином, щоб трафік з Client_2 до 172.17.D+10.1 проходив через Server_1, а до
172.17.D+20.1 через Net4. Для перевірки використати traceroute.

5. Розрахувати спільну адресу та маску (summarizing) адрес 172.17.D+10.1 та
172.17.D+20.1, при чому префікс має бути максимально можливим. Видалити
маршрути, встановлені на попередньому кроці та замінити їх об’єднаним
маршрутом, якій має проходити через Server_1.

6. Налаштувати SSH сервіс таким чином, щоб Client_1 та Client_2 могли
підключатись до Server_1 та один до одного.

7. Налаштуйте на Server_1 firewall таким чином:

• Дозволено підключатись через SSH з Client_1 та заборонено з Client_2
• З Client_2 на 172.17.D+10.1 ping проходив, а на 172.17.D+20.1 не проходив

8. Якщо в п.3 була налаштована маршрутизація для доступу Client_1 та Client_2 до
мережі Інтернет – видалити відповідні записи. На Server_1 налаштувати NAT
сервіс таким чином, щоб з Client_1 та Client_2 проходив ping в мережу Інтернет









