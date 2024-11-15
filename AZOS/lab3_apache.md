# 1 Задание


Установка Apache2

```bash
sudo apt update
sudo apt install apache2
```

Настройка хостов

```bash
takb@takb:/var/www/takb.com$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: wlp0s20f3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether e0:c2:64:c4:ff:09 brd ff:ff:ff:ff:ff:ff
    inet 192.168.4.210/24 brd 192.168.4.255 scope global dynamic noprefixroute wlp0s20f3
       valid_lft 3089sec preferred_lft 3089sec
    inet6 2a00:1fa0:4811:aeb1:e327:c4b:a2d8:e3f1/64 scope global temporary dynamic 
       valid_lft 7020sec preferred_lft 7020sec
    inet6 2a00:1fa0:4811:aeb1:b33d:d3e5:6cc1:4714/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 7020sec preferred_lft 7020sec
    inet6 fe80::d166:9374:eb6e:a3a9/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:42:f1:fc:64:21 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
takb@takb:/var/www/takb.com$ 

```

```bash 
takb@takb:/var/www/takb.com$ cat /etc/hosts
# /etc/hosts
192.168.4.210   takb.com www.takb.com
```

Создание ssl и подпись сертификата

```bash

```

Редактирование конфига сервера

```bash
# /etc/apache2/sites-available/takb.com.conf
<VirtualHost *:443>
    ServerName takb.com
    ServerAlias www.takb.com
    DocumentRoot /var/www/takb.com

    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/takb.com.crt
    SSLCertificateKeyFile /etc/apache2/ssl/takb.com.key
    SSLCACertificateFile /etc/apache2/ssl/my-ca.crt

    <Directory /var/www/takb.com>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Файлы на сервере

```bash
takb@takb:/var/www/takb.com$ tree
.
├── index.php
└── info.php

1 directory, 2 files
takb@takb:/var/www/takb.com$ 
```

```bash
takb@takb:/var/www/takb.com$ sudo service apache2 status
[sudo] пароль для takb: 
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/apache2.service; enabled; preset: >
     Active: active (running) since Fri 2024-11-15 13:03:40 MSK; 1h 10min ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 2732188 ExecStart=/usr/sbin/apachectl start (code=exited, status=0>
   Main PID: 2732191 (apache2)
      Tasks: 7 (limit: 18771)
     Memory: 21.9M (peak: 22.4M)
        CPU: 304ms
     CGroup: /system.slice/apache2.service
             ├─2732191 /usr/sbin/apache2 -k start
             ├─2732193 /usr/sbin/apache2 -k start
             ├─2732194 /usr/sbin/apache2 -k start
             ├─2732195 /usr/sbin/apache2 -k start
             ├─2732196 /usr/sbin/apache2 -k start
             ├─2732197 /usr/sbin/apache2 -k start
             └─2733173 /usr/sbin/apache2 -k start

ноя 15 13:03:39 takb systemd[1]: Starting apache2.service - The Apache HTTP Ser>
ноя 15 13:03:40 takb systemd[1]: Started apache2.service - The Apache HTTP Serv>
lines 1-20/20 (END)
```





