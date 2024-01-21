
## DNS Enumeration
There are multiple DNS record Type:
1. *NS* : It records nameserver records that contain domain
2. *CNAME* : it is used to create alias for a domain
3. *A* :  map domain to IPv4
4. *AAAA* : map domain to IPv6
5. *MX* : It is use for Mail Exchange record, and it can be multiple
6. *TXT* : It can contain any arbitrary data, used for domain ownership verification
7. *PTR* : It is used for reverse lookup, helpful when you IP and you want to know domain

using `host` command to find IP
`host megacorpone.com` will return the IP address of domain

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
we can scan port using nc. it's not for port scanning, but we can send them packets for connection and check whether port is open or not

`nc -nvv -w 1 -z ip port-range`: this will send SYN packet and try to make connection
`nc -nvv -w 1 -z -u ip port`: this can be used for checking UDP port but if port is closed it send ICMP packet of destination not found. If there is firewall or any configuration then it might not send ICMP packets, and it can show port is open

Now, we can use many tools for scanning port like nmap, masscan or rustscan
nmap can be run using with sudo or without sudo
when ran with *sudo* it uses _stealth scan_ by default `-sS`
when ran without *sudo* it uses _connect scan_ by default `-sT`

`-sT` for TCP connect scan
`-sS` for TCP stealth scan
`-sU` for UDP scan
`-sn` for network sweep we can give IP range
`--top-ports=20` for scanning top 20 ports
`-O` for OS scan it will only tell if it's 100% sure
`--osscan-guess` it will guess OS whether found or not
`-oG` for saving file
`-A` for running various scan
`-sV` for only just banners


windows:
`Test-NetConnection -Port 445 192.168.50.151`

## SMB Enumeration

SMB stands for Server Message Block protocol, always known for its poor security because of its complex implementation. It is used to share files between nodes in a network. It uses shared folder network to share

NetBIOS service listens on TCP 139, as well as several UDP ports, SMB (TCP 445) and NetBIOS are two separate protocols. NetBIOS is independent session layer protocol that allows a computer on local network whereas SMB earlier used to be dependent on NetBIOS, but newer version can run without NetBIOS.

Both services go hand-in-hand so we can scan together
`nmap -v -p 139,445 ip` will return Netbios and SMB port is open or not

there are tools for NetBIOS like `nbtscan`
`sudo nbtscan -r 192.168.50.0/24` will scan all NetBIOS on 192.168.50.0/24 range

we can use `enum4linux` for further scanning


## SMTP Enumeration

SMTP stands for Simple Mail Transfer Protocol
It has two jobs VRFY request and EXPN request
VRFY is use for verify existing users on mail server
EXPN asks the server for the membership of mailing server

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


## SNMP Enumeration

SNMP stands for Simple Network Management Protocol.
SNMP is based on UDP, a simple, stateless protocol, and is therefore susceptible to IP spoofing and replay attack. SNMP is used to monitor and manage the whole network. For example a building manager, how can he ensure that every floor, light and AC are working. If he's using something like SNMP he can know the details of every appliance, and its state.

SNMP uses community (Password) to manage its two roles
Read only: Default community is **public**
Read and Write: Default community is **private**
Manager: Default community is **manager**

Most of the time, people forget to change community. 

SNMP Management Information Base (MIB) is a database that contains information about network

| MIB  | Value  |
|---|---|
|1.3.6.1.2.1.25.1.6.0|System Processes|
|1.3.6.1.2.1.25.4.2.1.2|Running Programs|
|1.3.6.1.2.1.25.4.2.1.4|Processes Path|
|1.3.6.1.2.1.25.2.3.1.4|Storage Units|
|1.3.6.1.2.1.25.6.3.1.2|Software Name|
|1.3.6.1.4.1.77.1.2.25|User Accounts|
|1.3.6.1.2.1.6.13.1.3|TCP Local Ports|

`sudo nmap -sU -p 161 ip`: will check for open SNMP port
Alternatively, we can use `onesixtyone` to scan the SNMP server
```bash
kali@kali:~$ echo public > community
kali@kali:~$ echo private >> community
kali@kali:~$ echo manager >> community

kali@kali:~$ for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips

kali@kali:~$ onesixtyone -c community -i ips
Scanning 254 hosts, 3 communities
192.168.50.151 [public] Hardware: Intel64 Family 6 Model 79 Stepping 1 AT/AT COMPATIBLE - Software: Windows Version 6.3 (Build 17763 Multiprocessor Free)
```
This will show all open SNMP IP

We can use snmpwalk to interact with snmp server 
`snmpwalk -c public -v 1 -t 10 ip`: this will print information related to SNMP server
we can use SNMP MIB to get more information like process running, port or installed programs.
```bash
snmpwalk -c public -v 1 ip 1.3.6.1.4.1.77.1.2.25 # fetch all users
snmpwalk -c public -v 1 ip 1.3.6.1.2.1.25.4.2.1.2 # fetch all running process
```

You can also use `-Oa` for automatically converting hexadecimal to ASCII


