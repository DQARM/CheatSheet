## Use SMB ##
smbclient -L //IP -U DC_name\\acount  
smbclient //IP/<Folder> -U DC_name\\account  
smbclient //192.168.1.1/C$ -U DC_name\\account  

## Download File ##
certutil -urlcache -split -f <URL> <輸出檔名>

