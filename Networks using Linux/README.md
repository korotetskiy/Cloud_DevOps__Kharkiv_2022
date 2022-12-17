<h2>Networks using Linux</h2>
<head>
Практична частина модуля Linux Networking  передбачає створення засобами Virtual Box мережі, що показаний на малюнку
</br><img src="https://github.com/korotetskiy/img/blob/main/n1.png"><img src="https://github.com/korotetskiy/img/blob/main/n1-1.png"><img src="https://github.com/korotetskiy/img/blob/main/n1-2.png"><img src="https://github.com/korotetskiy/img/blob/main/n1-3.png">
Host – це комп’ютер, на якому запущений Virtual Box;</br>
Server_1  – Віртуальна машина, на якій розгорнуто ОС Linux. Int1 цієї машини в режимі «Мережевий міст» підключений до мережі Net1, тобто знаходиться в адресному просторі  домашньої  мережі.</br>
IP-адреса  Int1  встановлюється  статично  відповідно  до адресного  простору,  наприклад  192.168.1.200/24.</br>  
Iнтерфейси  Int2  та  Int3  відповідно підключено в режимі «Внутрішня мережа» до мереж Net2 та Net3.</br>
Client_1 та Client_2 – Віртуальні машини, на яких розгорнуто ОС Linux. </br> 
Інтерфейси  підключені  в  режимі «Внутрішня мережа» до мереж Net2, Net3 та Net4 як показано на рисунку</br>
<h4>Адреса  мережі Net2 –10.10.2.0/24,</h4>
<h4>Адреса мережі  Net3 –10.90.3.0/24,</h4>
<h4>Адреса мережі Net4 –172.16.6.0/24.</h4>
<h3>1. На Server_1 налаштувати статичні адреси на всіх інтерфейсах.</h3><img src="https://github.com/korotetskiy/img/blob/main/n2.png">
<h3>2. На  Server_1  налаштувати  DHCP  сервіс,  який  буде  конфігурувати  адреси  Int1 Client_1 та Client_2.
</h3><h4>sudo apt install isc-dhcp-server</h4>
<h4>Включаємо підтримку пересилання пакетів на всіх віртуальних хостах /etc/sysctl.conf, щоб трафік міг ходити між різними мережевими інтерфейсами.<br>
nano /etc/sysctl.conf<br>	
net.ipv4.conf.all.forwarding=1</h4><img src="https://github.com/korotetskiy/img/blob/main/n3-dhcp.png"> </h3><img src="https://github.com/korotetskiy/img/blob/main/n3-dhcp2.png"></h3><img src="https://github.com/korotetskiy/img/blob/main/n4-DHCP.png">
<h3>3. За  допомогою  команд  ping  та  traceroute перевірити  зв'язок  між  віртуальними машинами.</h3><img src="https://github.com/korotetskiy/img/blob/main/n1-ping.png"><img src="https://github.com/korotetskiy/img/blob/main/n1-2- ping.png"><img src="https://github.com/korotetskiy/img/blob/main/n3-dhcp-cl1.png"><img src="https://github.com/korotetskiy/img/blob/main/n1-trace.png">
<h3>4. На  віртуальному  інтерфейсу  lo Client_1 призначити дві ІР  адреси  за  таким правилом:  172.17.16.1/24 та 172.17.26.1/24.  Налаштувати  маршрутизацію таким чином, щоб трафік з Client_2 до 172.17.16.1 проходив через Server_1, а до 172.17.26.1 через Net4. Для перевірки використати traceroute.</h3><img src="https://github.com/korotetskiy/img/blob/main/n4.png"><img src="https://github.com/korotetskiy/img/blob/main/n4-1.png">
<h3>5.Розрахувати  спільну  адресу  та  маску  (summarizing) адрес  172.17.16.1 та 172.17.26.1,  при  чому префіксмає  бути  максимально  можливим.  Видалити маршрути,  встановлені  на  попередньому  кроці  та  замінити  їх  об’єднаним маршрутом, якій має проходити через Server_1.</h3><img src="https://github.com/korotetskiy/img/blob/main/n5.png"><img src="https://github.com/korotetskiy/img/blob/main/n5-3.png">
<h3>6.Налаштувати  SSH  сервіс  таким  чином,  щоб  Client_1  та  Client_2  могли підключатись до Server_1 та один до одного.</h3> 
На віртуальних хостах Server_1, Client_1 та Client_2  встановлюємо пакет openssh-server:</br>
<h4>sudo apt update</br>
sudo apt install openssh-server</br>
sudo systemctl status ssh</br>
sudo ufw enable</br>
sudo ufw allow ssh</br>
sudo ufw allow 22/tcp</h4>
<img src="https://github.com/korotetskiy/img/blob/main/n6-4.png">
Виконуємо аналогічно на хостах Client_1 та Client_2<img src="https://github.com/korotetskiy/img/blob/main/n6-5.jpg"> 
Перевіряємо доступ <img src="https://github.com/korotetskiy/img/blob/main/n6-6.png"><img src="https://github.com/korotetskiy/img/blob/main/n6-8.png">   
<h3>7.Налаштуйте на Server_1 firewall таким чином:</h3>
<h4>• Дозволено підключатись через SSH з Client_1 та заборонено з Client_2</h4>
<h4>• Client_2 на 172.17.16.1 ping  проходив, а на 172.17.26.1 не проходив</h4>
На віртуальнону хостi Server_1 додаємо правила для Client_1(10.10.2.10) та Client_2(10.10.2.10)</br>
<h4>sudo ufw allow from 10.10.2.10 to any port 22</br>
sudo ufw deny from 10.10.2.11 to any port 22</br>
<img src="https://github.com/korotetskiy/img/blob/main/n7-0.png"><img src="https://github.com/korotetskiy/img/blob/main/n7-2.png">
	


<h3>8.Якщо в п.3 була налаштована маршрутизація для доступу Client_1 та Client_2 до мережі  Інтернет – видалити  відповідні  записи.  На Server_1 налаштувати NATсервіс таким чином, щоб з Client_1 та Client_2 проходив ping в мережу Інтернет
sudo ufw allow from 10.10.2.10 to any port 22
sudo ufw deny from 10.10.2.11 to any port 22


очистить существующие NAT правила:
	
iptables -t nat --flush


iptables добавить правило, например:
iptables -t nat -A POSTROUTING -s 192.168.99.0/24 -j SNAT --to-source 172.16.16.94

Где, 192.168.99.0/24 внутренняя сеть, а 172.16.16.94 адрес через который нужно идти в интернет, аналогично прописываются другие внутренние сети.

Если IP адрес на внешнем сетевом интерфейсе меняется (динамический), тогда вместо SNAT укажем MASQUERADE:
1
	
iptables -t nat -A POSTROUTING -s 192.168.99.0/24 -j MASQUERADE


post-up /sbin/iptables -t nat -A POSTROUTING -s 192.168.99.0/24 -o eth3 -j SNAT --to-source 172.16.90.1-172.16.90.5 --persistent

