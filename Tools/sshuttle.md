# 先決條件  
SSH Server端有root權限  

## Topology  
10.10.14.22 <--> 10.129.247.87 <--> 172.16.5.19  

## Server  
```sshuttle -r forwarder Target ```  
```sshuttle -r admin@192.168.1.1 10.0.1.1 ```  

## RDP  
```xfreerdp3 /v:172.16.5.19 /u:victor /p:'pass@123'```  

## Server snapshot  
<img width="1341" height="107" alt="image" src="https://github.com/user-attachments/assets/055a7c4d-def2-42f8-9fb5-e4d5d0f12d6a" />  
