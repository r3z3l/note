
## OS Command Injection


Many times web application needs to interact to OS and developers directly takes users input, sanitize it and prepare it to interact with OS.
This can lead to security issues of OS command injection.


Note: we can use `;`, `&&`, `&` to pass other command after command if required. There could be more way


```powershell
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```
This cmd can be useful to identify shell type in windows