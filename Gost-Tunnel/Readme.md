## Installing Section 1st way
```
apt install golang-go && install gccgo-go && git clone https://github.com/go-gost/gost.git && cd gost/cmd/gost && go build
```
=========================================
## Installing Section 2nd way
```
apt install wget -y && wget https://github.com/go-gost/gost/releases/download/v3.0.0-rc6/gost_3.0.0-rc6_linux_amd64.tar.gz && mkdir /usr/local/bin/gost && tar -xvzf gost_3.0.0-rc6_linux_amd64.tar.gz -C /usr/local/bin/gost/ && chmod +x /usr/local/bin/gost/
```
=========================================
## Configure Gost Service
```
nano /usr/lib/systemd/system/gost.service
```
### replace below without any changes
```
[Unit]
Description=GO Simple Tunnel
After=network.target
Wants=network.target
 
[Service]
Type=simple
ExecStart=/usr/local/bin/gost/gost
 
[Install]
WantedBy=multi-user.target
```
### Reload daemon and start gost
``` 
systemctl daemon-reload && systemctl start gost
```
### now check the status to verify its running
```
systemctl status gost
```
### to restart the service
```
systemctl restart gost
```
=========================================
## Config the service to connect tunnel 

### Method A - Http Proxy

### Relay Server Or Iran Server
``` 
-L=http://:443 -F http://IP-Kharej:443
``` 
### Proxy Server Or Kharej Server
``` 
-L=http://:443 -F http://IP-Kharej:443
``` 
=========================================
### Method B - Wss+Relay

### Relay Server Or Iran Server
``` 
-L=tcp://:8080 -F relay+wss://:8420
```
### Proxy Server Or Kharej Server
``` 
-L=relay+wss://8429/:18080
``` 
=========================================
### Method C - kcp tunnel

### Relay Server Or Iran Server
``` 
-L=tcp://127.0.0.1:8083  -F forward+kcp://Server-Kharej:9000
```
### Proxy Server Or Kharej Server
```
-L=kcp://:9000/:8083 
```
### Udp Port should be open on firewall
 
=========================================
### Method C - kcp+Relay

### Relay Server Or Iran Server
```
-L tcp://:Port-v2ray/127.0.0.1:Port-v2ray -F relay+kcp://IP-Kharej:7079
```
### Proxy Server Or Kharej Server
```
-L relay+kcp://:7079
```
==================================================
### Source
 
https://gost.run/en/
https://github.com/woodlyer/gostExample
