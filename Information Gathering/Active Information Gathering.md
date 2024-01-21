
## DNS Enumeration
There are multiple DNS record Type:
1. *NS* : It records nameserver records that contain domain
2. *CNAME* : it is used to create alias for a domain
3. *A* :  map domain to IPv4
4. *AAAA* : map domain to IPv6
5. *MX* : It is use for Mail Exchange record and it can be multiple
6. *TXT* : It can contain any arbitary data, used for domain ownership verification
7. *PTR* : It is used for reverse lookup, helpful when you IP and you want to know domain

using `host` command to find ip
`host megacorpone.com` will return the ip address of domain

we can also add some flags like
`-t` for specifying record type


_Tools_ :
We have two famous tools:
- **DNSRecon**
		`dnsrecon -d megacorpone.com -t std` for running standard DNS scan on megacorpone.com
		`dnsrecon -d megacorpone.com -D ~/brute.txt -t brt` for running brute force scan on megacorpone.com
- **DNSEnum**
		`dnsenum megacorpone.com` to DNS scan on megacorpone.com 


## TCP/UDP Port Scanning
we can scan port using nc. it's not for port scanning but we can send them packets for connection and check whether port is open or not

`nc -nvv -w 1 -z ip port-range`: this will send SYN packet and try to make connection
`nc -nvv -w 1 -z -u ip port`: this can be used for checking UDP port but if port is closed it send ICMP packet of destination not found. if there is firewall or any configuration then it might not send ICMP packets and it can show port is open

Now, we can use many tools for scanning port like nmap, masscan or rustscan
nmap can be run using with sudo or without sudo
when ran with *sudo* it uses _stealth scan_ by default `-sS`
when ran without *sudo* it uses _connect scan_ by default `-sT`

`-sT` for TCP connect scan
`-sS` for TCP stealth scan
`-sU` for UDP scan
`-sn` for network sweep we can give ip range
`--top-ports=20` for scanning top 20 ports
`-O` for OS scan it will only tell if it's 100% sure
`--osscan-guess` it will guess os whether foudn or not
`-oG` for saving file
`-A` for running various scan
`-sV` for only just banners


windows:
`Test-NetConnection -Port 445 192.168.50.151`

