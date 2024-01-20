
## Whois 
[_Whois_](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/information-gathering/passive-information-gathering/whois-enumeration#fn1) is a TCP service, tool, and type of database that can provide information about a domain name, such as the _name server_[2](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/information-gathering/passive-information-gathering/whois-enumeration#fn2) and _registrar_.[3](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/information-gathering/passive-information-gathering/whois-enumeration#fn3) This information is often public, since registrars charge a fee for private registration.
`whois megacorpone.com -h 192.168.50.251`

It can also be used to perform reverse lookup if we have an ip address
	`whois 38.100.193.70 -h 192.168.50.251

## Google Hacking / Dorking


![[Pasted image 20240120234333.png]]

Some Resource :
1. [Exploit DB google dorking](https://www.exploit-db.com/google-hacking-database)
2. [DorkSearch](https://dorksearch.com/)

## NetCraft
_Netcraft_[1](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/information-gathering/passive-information-gathering/netcraft#fn1) is an internet service company, based in England, offering a free web portal that performs various information gathering functions such as discovering which technologies are running on a given website and finding which other hosts share the same IP netblock.


helps you get the hosted ip address, DNS server name, application servers and technology running

1. [NetCraft](https://searchdns.netcraft.com)

## Open-Source Code
Trying to check for its repository on Opensource platform like github
using tools like gitleaks or gitrob


## Shodan
It crawls for all internet-connected device, like servers running website, IoT gadgets and display them

## Security Headers and SSL/TLS
[Security Headers](https://securityheaders.com/) check for website 
[SSL/TLS](https://www.ssllabs.com/ssltest/) check for website. It can also identify vulnerabilities like Poodle or HeartBleed
