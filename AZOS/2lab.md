# ЛР №2
#### Чумаченко Александр А-07-22
<br><br>



<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 1</p>

---

#### 1. Объясните результат выполнения команды: ping example.com.
```
astravmuser@astravm-23-28:~$ sudo nano /etc/hosts
astravmuser@astravm-23-28:~$ ping example.com
PING example.com (192.168.56.101) 56(84) bytes of data.
64 bytes from example.com (192.168.56.101): icmp_seq=1 ttl=64 time=0.016 ms
64 bytes from example.com (192.168.56.101): icmp_seq=2 ttl=64 time=0.021 ms
64 bytes from example.com (192.168.56.101): icmp_seq=3 ttl=64 time=0.024 ms
64 bytes from example.com (192.168.56.101): icmp_seq=4 ttl=64 time=0.020 ms
```

Команда пинг отправляет пакеты на днс адрес, в данном случае example.com, привязынный к локальному ip адресу. И получает ответные данные, если связь установлена.

---
#### 2. Перечислите параметры: имя интерфейса, MAC и IP адрес для интерфейса, используемого в лабораторной работе.
```
astravmuser@astravm-23-28:~$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host  
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:0b:00:7b brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute eth0
       valid_lft 85536sec preferred_lft 85536sec
    inet6 fe80::645f:ddd9:ca79:cfad/64 scope link noprefixroute         valid_lft forever preferred_lft forever
```

Имя интерфейса: eth0

MAC: 08:00:27:0b:00:7b

IP: 10.0.2.255

---

<p style="color: aqua; font-weight: bold; font-size: 20px;">Часть 2</p>

---

#### 1.Выполните трассировку до узла mpei.ru и объясните результат (количество промежуточных узлов и задержки до каждого).

```
astravmuser@astravm-23-28:~$ sudo traceroute -I mpei.ru
 1  10.0.2.2 (10.0.2.2)  0.143 ms  0.124 ms *
 2  192.168.64.231 (192.168.64.231)  4.864 ms * *
 3  172.16.9.138 (172.16.9.138)  31.891 ms * *
 4  172.16.13.85 (172.16.13.85)  43.764 ms * *
 5  * * *
 6  a433-cr06-eth-trunk55.msk.mts-internet.net (212.188.42.41)  44.983 ms * *
 7  m9-cr02-be7.msk.mts-internet.net (195.34.53.204)  396.435 ms  50.652 ms  50.788 ms
 8  as3267.asbr.router (212.188.33.181)  50.783 ms * *
 9  46.lt000.m9-1-gw.msk.niks.su (194.190.255.50)  36.433 ms * *
10  core-145.mpei.ac.ru (193.233.67.145)  23.303 ms * *
11  core-135.mpei.ac.ru (193.233.67.135)  158.588 ms  158.812 ms *
12  srv68-141.mpei.ac.ru (193.233.68.141)  158.578 ms  38.240 ms  38.393 ms
```


#### 2. Запустите iperf в режиме клиента и сервера, выполните тест на пропускную способность в течение 10 секунд, и объясните результаты (средняя скорость передачи данных, потери пакетов).

```
astravmuser@astravm-23-28:~$ iperf -s            
------------------------------------------------------------
Server listening on TCP port 5001
TCP window size:  128 KByte (default)
------------------------------------------------------------
[  4] local 10.0.2.15 port 5001 connected with 10.0.2.15 port 36314
[ ID] Interval       Transfer     Bandwidth
[  4]  0.0-10.0 sec  65.7 GBytes  56.4 Gbits/sec


astravmuser@astravm-23-28:~$ iperf -c 10.0.2.15 -p 5001 -t 10
------------------------------------------------------------
Client connecting to 10.0.2.15, TCP port 5001
TCP window size: 2.50 MByte (default)
------------------------------------------------------------
[  3] local 10.0.2.15 port 36314 connected with 10.0.2.15 port 5001
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  65.7 GBytes  56.4 Gbits/sec
```