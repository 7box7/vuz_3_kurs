# Настройка почты


## 1. Работа Postfix и Dovecot:

### Работоспособность
```bash
~ ❯ sudo systemctl status postfix                                                                                                                                                                  20:21:27
sudo systemctl status dovecot
● postfix.service - Postfix Mail Transport Agent
     Loaded: loaded (/usr/lib/systemd/system/postfix.service; enabled; preset: enabled)
     Active: active (exited) since Thu 2024-12-12 20:12:05 MSK; 9min ago
       Docs: man:postfix(1)
   Main PID: 1556048 (code=exited, status=0/SUCCESS)
        CPU: 2ms

дек 12 20:12:05 takb systemd[1]: Starting postfix.service - Postfix Mail Transport Agent...
дек 12 20:12:05 takb systemd[1]: Finished postfix.service - Postfix Mail Transport Agent.
● dovecot.service - Dovecot IMAP/POP3 email server
     Loaded: loaded (/usr/lib/systemd/system/dovecot.service; enabled; preset: enabled)
     Active: active (running) since Thu 2024-12-12 20:16:16 MSK; 5min ago
       Docs: man:dovecot(1)
             https://doc.dovecot.org/
   Main PID: 1556326 (dovecot)
     Status: "v2.3.21 (47349e2482) running"
      Tasks: 4 (limit: 18776)
     Memory: 3.6M (peak: 3.9M)
        CPU: 58ms
     CGroup: /system.slice/dovecot.service
             ├─1556326 /usr/sbin/dovecot -F
             ├─1556329 dovecot/anvil
             ├─1556330 dovecot/log
             └─1556331 dovecot/config

дек 12 20:16:16 takb systemd[1]: Starting dovecot.service - Dovecot IMAP/POP3 email server...
дек 12 20:16:16 takb dovecot[1556326]: master: Dovecot v2.3.21 (47349e2482) starting up for imap, pop3, lmtp, imap, lmtp, pop3 (core dumps disabled)
дек 12 20:16:16 takb systemd[1]: Started dovecot.service - Dovecot IMAP/POP3 email server.
~ ❯   
```  

### Порты

```bash
~ ❯ netstat -tuln | grep -E '25|143|110'                                                                                                                                                           20:22:32
tcp        0      0 0.0.0.0:143             0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:25              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:110             0.0.0.0:*               LISTEN     
tcp6       0      0 :::143                  :::*                    LISTEN     
tcp6       0      0 :::25                   :::*                    LISTEN     
tcp6       0      0 :::110                  :::*                    LISTEN     
udp        0      0 192.168.1.255:137       0.0.0.0:*                          
udp        0      0 172.17.255.255:137      0.0.0.0:*                          
udp        0      0 192.168.1.255:138       0.0.0.0:*                          
udp        0      0 172.17.255.255:138      0.0.0.0:*                          
udp6       0      0 :::52548                :::*                               
~ ❯    
```

## 2. Настроенные почтовые учетные записи



