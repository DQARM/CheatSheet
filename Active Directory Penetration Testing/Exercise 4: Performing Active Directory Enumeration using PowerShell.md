[Powerview.ps1](https://github.com/PowerShellMafia/PowerSploit/tree/master/Recon)
### Import Powerview.ps1 ###
Powershell -ep bypass

Import-Module .\Powerview.ps1  

### Enumeration ###
Get-Domain
Get-Domaincomputer
Get-DomainGroup
Get-DomainPolicy
Get-NetUser
Get-Netuser --Properties name
Get-Netuser --Properties name, pwdlastset

### AES-Roastable ###
## 出現DONT_REQ_PREAUTH的就是可以AES-Roasting的 ##
Get-Netuser -properties name,Useraccountcontrol






