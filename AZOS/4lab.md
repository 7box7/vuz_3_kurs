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
### Assigning static IP-address
### Check logs 

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
### Available Samba-server
### Available Kerberos-auth
### Allow to common folder
### Check logs


## Task 4. Diagnosing and troubleshooting FreeIPA and Samba setup errors

### Config's error
### Using diagnostics tools
### Bug fixes
### Available after bug fixes

 