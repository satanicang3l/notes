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
If you want to perform DNS transfer on a certain zone, use:\
`dig AXFR @example.com zonename`\
To get the bind version, use:\
`dig chaos txt version.bind @example.com`