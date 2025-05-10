---
title: Port Scanning
parent: Recon
nav_order: 1
---

1. AutoRecon: `autorecon -v IP`
2. Nmap: (USE IP instead of domain name as might miss information or scan both)
  - Standard TCP port (change sT to sU for UDP): `nmap -n -v -sT -A IP`
  - Full TCP (change sT to sU for UDP): `nmap -n -v -sT -p- -T5 IP`
  - Using results from b.: `nmap -n -v -sT -p ports from b. -A IP`
  - Vulnerability scan: `nmap -sV -sT -pPort --script vuln IP`
  - Backup: `nmap -p- --min-rate 5000 -sV IP2`
  - Default script: `sudo nmap -sC -sS -p0-65535 IP`
  - Limited scan (eg for 2 host): `nmap --top-ports=1000 -sT -Pn 10.5.5.1,2 --open`


## Limited Scan
`proxychains4 nmap --top-ports=100 -sT -Pn IP --open`