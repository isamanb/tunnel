### Enable IP Forwarding
```
sudo sysctl net.ipv4.ip_forward=1
```
### Rules Modify "IP-Iran" and "IP-Kharej" with your IP addresses
```
iptables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination IP-Iran
iptables -t nat -A PREROUTING -j DNAT --to-destination IP-Kharej
iptables -t nat -A POSTROUTING -j MASQUERADE
```
--------------------------------------------------------------------------------------------------------
### Save the rules to start as boot service

### Method A 
```
sudo sh -c "iptables-save > /etc/iptables.rules" && nano /etc/network/interfaces
```
### Add below to the file
```
pre-up iptables-restore < /etc/iptables.rules
```
-------------------------------------------------------------------------------------------------------
### Method B
```
nano /etc/rc.local
```
### Add below to the file (remember to change "IP-Iran" and "IP-Kharej")

```
#! /bin/bash
sysctl net.ipv4.ip_forward=1
iptables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination IP-Iran
iptables -t nat -A PREROUTING -j DNAT --to-destination IP-Kharej
iptables -t nat -A POSTROUTING -j MASQUERADE
exit 0
```
### After saving above file then
```
chmod +x /etc/rc.local
``` 
--------------------------------------------------------------------------------------------------
## To verify saved rules PreRouting
```
iptables -L -v
```
```
iptables -L -n -t nat
```
