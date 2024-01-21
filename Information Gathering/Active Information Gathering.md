
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

## SMB Enumeration

SMB stands for Server Message Block protocol always known for it's poor security because of its complex implementation. It is use to share files between nodes in a network. it uses shared folder network to share

NetBIOS service listens on TCP 139, as well as several UDP ports, SMB (TCP 445) and NetBIOS are two separate protocols. NetBIOS is independent session layer protocol that allows a computer on local network whereas SMB earlier used to be dependend on NetBIOS but newer version can run without NetBIOS.

both services go hand-in-hand so we can scan together
`nmap -v -p 139,445 ip` will return Netbios and SMB port is open or not

there are tools for NetBIOS like `nbtscan`
`sudo nbtscan -r 192.168.50.0/24` will scan all NetBIOS on 192.168.50.0/24 range

we can use `enum4linux` for further scanning


## SMTP Enumeration

SMTP stands Simple Mail Transfer Protocol
It has two jobs VRFY request and EXPN request
VRFY is use for verify existing users on mail server
EXPN asks the server for the membarship of mailing server

we can connect using `nc` and check whether user exists or not
```bash
kali@kali: ~$ nc -nv 192.168.192.8 25
(UNKNOWN) [192.168.192.8] 25 (smtp) open
220 mail ESMTP Postfix (Ubuntu)
VRFY root
252 2.0.0 root
VRFY hk
550 5.1.1 <hk>: Recipient address rejected: User unknown in local recipient table

```
