---
title: Subdomain / Vhosts
parent: Recon
nav_order: 6
---

Vhosts means same IP and server, but otherwise same as subdomain.

`ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://example.com:PORT -H 'Host: FUZZ.example.com`
