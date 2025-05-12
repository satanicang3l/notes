---
title: DNS
parent: Recon
nav_order: 5
---

Get IP from hostname:\
`nslookup hostname.workgroup.service`


If want to get TXT record, use the following:\
`dig -t TXT example.com`


For zone transfers, use\
`dig AXFR example.com`\
If this fails, first get the DNS server use by the zone directly:\
`dig -t SOA example.com`\
The DNS server is in the NS response. If no NS response can try to use back the address you have (which is example.com in this case). Use this DNS server to perform zone transfer:\
`dig AXFR example.com @dnsserver.com`\
If you see some internal subdomain like internal.example.com, can further attempt to perform zone transfer:\
`dig AXFR internal.example.com @dnsserver.com`\
If you want to perform DNS transfer on a certain zone, use:\
`dig AXFR @example.com zonename`\
To get the bind version, use:\
`dig chaos txt version.bind @example.com`

Dig ALL/ANY records:\
`dig ANY domain.local @10.10.25.23`\
In this case, domain.local is the domain name and 10.10.25.23 is the DNS server.

To find out more information, for example IP and hostname, can use DNSEnum. But need to add the DNS to host entry first:\
`sudo sh -c 'echo "DNSSERVERIP internal.inlanefreight.htb" >> /etc/hosts'`\
Then run dnsenum:\
`dnsenum --dnsserver DNSSERVERIP --enum -p 0 -s 0 -f /usr/share/seclists/Discovery/DNS/namelist.txt TryAllDomainNameIncludingInternal`\
For example:\
`dnsenum --dnsserver 10.10.25.23 --enum -p 0 -s 0 -f /usr/share/seclists/Discovery/DNS/namelist.txt dev.inlanefreight.htb`
