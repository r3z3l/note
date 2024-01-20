
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
