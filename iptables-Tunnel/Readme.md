### update and install iptables 
```
apt update && apt upgrade -y && apt install iptables && apt install iptables-persistent -y
```
### Enable IP Forwarding (IPV4)
```
sudo sysctl net.ipv4.ip_forward=1
```
### Enable IP Forwarding (IPV6)
```
sudo sysctl net.ipv6.ip_forward=1
```
### Rules Modify "IP-Iran" and "IP-Kharej" with your IP addresses (IPV4)
```
iptables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination IP-Iran
iptables -t nat -A PREROUTING -j DNAT --to-destination IP-Kharej
iptables -t nat -A POSTROUTING -j MASQUERADE
```
### Rules Modify "IP-Iran" and "IP-Kharej" with your IP addresses (IPV6)
```
ip6tables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination IP6-Iran
ip6tables -t nat -A PREROUTING -j DNAT --to-destination IP6-Kharej
ip6tables -t nat -A POSTROUTING -j MASQUERADE
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
### For IPV6
```
sudo sh -c "ip6tables-save > /etc/ip6tables.rules" && nano /etc/network/interfaces
```
### Add below to the file
```
pre-up ip6tables-restore < /etc/ip6tables.rules
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
### If using ipv4 and ipv6 togather 
```
#! /bin/bash
sysctl net.ipv4.ip_forward=1
iptables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination IP-Iran
iptables -t nat -A PREROUTING -j DNAT --to-destination IP-Kharej
iptables -t nat -A POSTROUTING -j MASQUERADE
ip6tables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination IP-Iran
ip6tables -t nat -A PREROUTING -j DNAT --to-destination IP-Kharej
ip6tables -t nat -A POSTROUTING -j MASQUERADE
exit 0
```
### After saving above file then
```
chmod +x /etc/rc.local
``` 
--------------------------------------------------------------------------------------------------
## To verify saved rules PreRouting (IPV4)
```
iptables -L -v
```
```
iptables -L -n -t nat
```
## To verify saved rules PreRouting (IPV6)
```
ip6tables -L -v
```
```
ip6tables -L -n -t nat
```
