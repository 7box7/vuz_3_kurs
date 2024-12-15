# Lab 4

## Task 1. Install DHCP-server

### Available DHCP-server
```bash
~ ❯ sudo systemctl status isc-dhcp-server                                                                                                                                                          
● isc-dhcp-server.service - ISC DHCP IPv4 server
     Loaded: loaded (/usr/lib/systemd/system/isc-dhcp-server.service; enabled; preset: enabled)
     Active: active (running) since Fri 2024-12-13 12:18:00 MSK; 32s ago
       Docs: man:dhcpd(8)
   Main PID: 7177 (dhcpd)
      Tasks: 1 (limit: 18776)
     Memory: 3.7M (peak: 4.0M)
        CPU: 14ms
     CGroup: /system.slice/isc-dhcp-server.service
             └─7177 dhcpd -user dhcpd -group dhcpd -f -4 -pf /run/dhcp-server/dhcpd.pid -cf /etc/dhcp/dhcpd.conf wlp0s20f3

дек 13 12:18:00 mail.vmss.local sh[7177]: Wrote 0 leases to leases file.
дек 13 12:18:00 mail.vmss.local dhcpd[7177]: PID file: /run/dhcp-server/dhcpd.pid
дек 13 12:18:00 mail.vmss.local dhcpd[7177]: Wrote 0 leases to leases file.
дек 13 12:18:00 mail.vmss.local dhcpd[7177]: Listening on LPF/wlp0s20f3/e0:c2:64:c4:ff:09/192.168.1.0/24
дек 13 12:18:00 mail.vmss.local sh[7177]: Listening on LPF/wlp0s20f3/e0:c2:64:c4:ff:09/192.168.1.0/24
дек 13 12:18:00 mail.vmss.local sh[7177]: Sending on   LPF/wlp0s20f3/e0:c2:64:c4:ff:09/192.168.1.0/24
дек 13 12:18:00 mail.vmss.local sh[7177]: Sending on   Socket/fallback/fallback-net
дек 13 12:18:00 mail.vmss.local dhcpd[7177]: Sending on   LPF/wlp0s20f3/e0:c2:64:c4:ff:09/192.168.1.0/24
дек 13 12:18:00 mail.vmss.local dhcpd[7177]: Sending on   Socket/fallback/fallback-net
дек 13 12:18:00 mail.vmss.local dhcpd[7177]: Server starting service.
~ ❯      
```

### Setup IP-addresses range
```bash
# A slightly different configuration for an internal subnet.
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.150 192.168.1.180;
  option domain-name-servers 192.168.1.222;
  option domain-name "vmss.local";
  option subnet-mask 255.255.255.0;
  option routers 192.168.1.1;
  option broadcast-address 192.168.1.222;
  default-lease-time 6000;
  max-lease-time 7200;
}
```

### Assigning IP-addresses to clients

```bash
astravmuser@astravm:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:31:a3:e7 brd ff:ff:ff:ff:ff:ff
    inet 192.168.106.50/24 brd 192.168.106.255 scope global noprefixroute eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::643e:22c9:9efd:966a/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
astravmuser@astravm:~$ 
```

### Assigning static IP-address

```bash
astravmuser@astravm:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:31:a3:e7 brd ff:ff:ff:ff:ff:ff
    inet 192.168.106.50/24 brd 192.168.106.255 scope global noprefixroute eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::643e:22c9:9efd:966a/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
astravmuser@astravm:~$ 
``` 


## Task 2. Install DNS-server

### Available DNS-server

```bash
~ ❯ sudo systemctl status bind9                                                                                                                                                                    
● named.service - BIND Domain Name Server
     Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; preset: enabled)
     Active: active (running) since Fri 2024-12-13 12:07:43 MSK; 13min ago
       Docs: man:named(8)
   Main PID: 6262 (named)
     Status: "running"
      Tasks: 38 (limit: 18776)
     Memory: 13.7M (peak: 16.4M)
        CPU: 433ms
     CGroup: /system.slice/named.service
             └─6262 /usr/sbin/named -f -u bind

дек 13 12:07:43 mail.vmss.local named[6262]: zone 0.in-addr.arpa/IN: loaded serial 1
дек 13 12:07:43 mail.vmss.local named[6262]: zone 255.in-addr.arpa/IN: loaded serial 1
дек 13 12:07:43 mail.vmss.local named[6262]: zone localhost/IN: loaded serial 2
дек 13 12:07:43 mail.vmss.local named[6262]: zone 127.in-addr.arpa/IN: loaded serial 1
дек 13 12:07:43 mail.vmss.local named[6262]: all zones loaded
дек 13 12:07:43 mail.vmss.local named[6262]: running
дек 13 12:07:43 mail.vmss.local systemd[1]: Started named.service - BIND Domain Name Server.
дек 13 12:07:43 mail.vmss.local named[6262]: managed-keys-zone: Key 20326 for zone . is now trusted (acceptance timer complete)
дек 13 12:07:43 mail.vmss.local named[6262]: resolver priming query complete: success
дек 13 12:20:59 mail.vmss.local named[6262]: timed out resolving 'accounts.google.com/HTTPS/IN': 8.8.8.8#53
~ ❯                                                                                                                                                                                                
```
### Main zone

```bash
~ ❯ nslookup                                                                                                                                                                                      
> google.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	google.com
Address: 64.233.161.138
Name:	google.com
Address: 64.233.161.101
Name:	google.com
Address: 64.233.161.102
Name:	google.com
Address: 64.233.161.100
Name:	google.com
Address: 64.233.161.113
Name:	google.com
Address: 64.233.161.139
Name:	google.com
Address: 2a00:1450:4010:c0e::64
Name:	google.com
Address: 2a00:1450:4010:c0e::65
Name:	google.com
Address: 2a00:1450:4010:c0e::71
Name:	google.com
Address: 2a00:1450:4010:c0e::8a
> yandex.ru
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	yandex.ru
Address: 77.88.44.55
Name:	yandex.ru
Address: 77.88.55.88
Name:	yandex.ru
Address: 5.255.255.77
Name:	yandex.ru
Address: 2a02:6b8:a::a
> 
```
### Back BIND

```bash
~ ❯ nslookup 192.168.1.222                                                                                                                                                                        
222.1.168.192.in-addr.arpa	name = mail.vmss.local.
222.1.168.192.in-addr.arpa	name = mail.
222.1.168.192.in-addr.arpa	name = mail.local.

~ ❯    
```
### Redirect request

```
~ ❯ nslookup google.com 127.0.0.1                                                                                                                                                                  
Server:		127.0.0.1
Address:	127.0.0.1#53

Non-authoritative answer:
Name:	google.com
Address: 74.125.131.138
Name:	google.com
Address: 74.125.131.101
Name:	google.com
Address: 74.125.131.102
Name:	google.com
Address: 74.125.131.100
Name:	google.com
Address: 74.125.131.113
Name:	google.com
Address: 74.125.131.139
Name:	google.com
Address: 2a00:1450:4010:c0e::65
Name:	google.com
Address: 2a00:1450:4010:c0e::71
Name:	google.com
Address: 2a00:1450:4010:c0e::8a
Name:	google.com
Address: 2a00:1450:4010:c0e::64

~ ❯       
```

### Check logs

## Task 3. Install FreeIPA-server 

### Available FreeIPA-server
```bash
astravmuser@astravm:~$ sudo ipactl status
[sudo] пароль для astravmuser: 
Попробуйте ещё раз.
[sudo] пароль для astravmuser: 
Directory Service: RUNNING
krb5kdc Service: RUNNING
kadmin Service: RUNNING
named Service: RUNNING
httpd Service: RUNNING
ipa-custodia Service: RUNNING
pki-tomcatd Service: RUNNING
ipa-otpd Service: RUNNING
ipa-dnskeysyncd Service: RUNNING
ipa: INFO: The ipactl command was successful
```
### Available Samba-server

```bash
  GNU nano 3.2                                                                     /etc/samba/smb.conf                                                                               

### Added by IPA Installer ###
#         DO NOT EDIT        #
[global]
debug pid = yes
state directory = /var/lib/samba
cache directory = /var/lib/samba
include = registry
```

### Available Kerberos-auth
```bash
astravmuser@astravm:~$ ipa group-add vmss
-----------------------
Добавлена группа "vmss"
-----------------------
  Имя группы: vmss
  ID группы: 506800004
astravmuser@astravm:~$ ipa group-add-member vmss --users=vmss1, --user=vmss2
  Имя группы: vmss
  ID группы: 506800004
  Ошибка участников: 
    member user: vmss1,: no such entry
    member user: vmss2: no such entry
    member group: 
    member service: 
    member User ID override: 
-----------------------------------
Количество добавленных участников 0
-----------------------------------
astravmuser@astravm:~$ 
```
### Allow to common folder

### Check logs


## Task 4. Diagnosing and troubleshooting FreeIPA and Samba setup errors

### Config's error
### Using diagnostics tools
### Bug fixes
### Available after bug fixes

 