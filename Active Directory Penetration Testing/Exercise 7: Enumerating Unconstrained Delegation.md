### Windows ###
Import-Module .\Powerview.ps1 
 Get-Netcomputer -Unconstrained 
### Linux ###
nxc ldap <DC_IP> -u <user> -p '<pass>' --trusted-for-delegation
