# Discovered services 

Firstly we need to discover what services we are running.

This is done with `netstat -tulpn`.

```
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 192.168.7.200:27017     0.0.0.0:*               LISTEN      16734/mongod        
tcp        0      0 127.0.0.1:27017         0.0.0.0:*               LISTEN      16734/mongod        
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      687/rpcbind         
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      27643/nginx: master 
tcp        0      0 0.0.0.0:20048           0.0.0.0:*               LISTEN      1417/rpc.mountd     
tcp        0      0 0.0.0.0:9650            0.0.0.0:*               LISTEN      1326/lighttpd       
tcp        0      0 0.0.0.0:53              0.0.0.0:*               LISTEN      1624/pihole-FTL     
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1321/sshd           
tcp        0      0 0.0.0.0:1880            0.0.0.0:*               LISTEN      693/node-red        
tcp        0      0 192.168.7.200:1881      0.0.0.0:*               LISTEN      5458/node           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1693/master         
tcp        0      0 0.0.0.0:8123            0.0.0.0:*               LISTEN      24069/python3       
tcp        0      0 0.0.0.0:1883            0.0.0.0:*               LISTEN      2749/mosquitto      
tcp        0      0 192.168.7.200:8124      0.0.0.0:*               LISTEN      24069/python3       
tcp        0      0 127.0.0.1:8125          0.0.0.0:*               LISTEN      31774/netdata       
#IPv6 entries omitted except:
tcp6       0      0 :::8091                 :::*                    LISTEN      23379/docker-proxy
```

Above is a list of somewhat relevant ipv4 results. Let's go through the interesting ones:

### mongod
This one is actually already migrated and the one running here is an abandoned one. We can discard it.

### nginx
Nginx is acting as the front for all my homelab services, a lot of these are already transferred over but it needs to be finalized.

### lighttpd (& pihole-FTL)
Looking into /etc/lighttpd reveals that this is actually managed by pihole. Nowadays I use pfsense for my dns needs so this one is also defunct.

### node-red
This needs to be migrated and is tied to home assistant. 

### node
This one is not self-explanatory but the port number 1881 tells us that it is my zigbee2mqtt instance running. Needs to be migrated.

### master? Port 25
Don't really know as I don't recall having a mail server on here. Probably some experiment that I forgot to remove...

### 24069/python3 
This is home assistant as I've configured it on port 8123. To be migrated. Currently running inside docker already but using host networking if I recall correctly.

### netdata
Logging service I've used to investigate hardware problems but not needed now when running supervised and not bare-metal.

### mosquitto
MQTT broker that needs to be moved. A lot of my smart home stuff goes through MQTT (Z-Wave & Zigbee)

### docker-proxy on 8091
Checking `docker ps` tells us this is my zwave2mqtt server. Needs to be migrated.

## Find configs 
Next up I check the config location of every single program we want to migrate.

| Service        | Config Location                    |
|----------------|------------------------------------|
| home assistant | /home/homeassistant/.homeassistant |
| node-red       | /home/homeassistant/.nodered       |
| mosquitto      | /etc/mosquitto                     |
| zigbee2mqtt    | /home/homeassistant/zigbee2mqtt    |
| zwave2mqtt     | /home/homeassistant/zwave-js       |
| nginx          | /etc/nginx                         |
