### SSH to Relay (Iran) server with root previllage (remember to modify your IP with "IP-Kharej")
``` 
sudo ssh -f -N -L 0.0.0.0:8880:iP-Kharej:8880 root@iP-Kharej
```
## if everythings goes well then ctrl+c to exit above command and save as bash script to run with cronjob
```
nano /usr/local/bin/tunnel.sh
```
### Add below to the file (remember to modify your IP with "IP-Kharej")

```
#!/bin/sh
sudo iptables -t nat -A POSTROUTING -j MASQUERADE
sudo ssh -p 22 -f -N -L 0.0.0.0:8880:IP-Kharej:8880 root@IP-Kharej
```
```
chmod +x /usr/local/bin/tunnel.sh
```
### With cronjob set the time to start script after reboot
``` 
crontab -e
```
### Add this line to below the file
```
@reboot /usr/local/bin/tunnel.sh
```
