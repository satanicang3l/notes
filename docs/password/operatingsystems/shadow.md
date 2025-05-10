---
title: /etc/shadow
parent: Operating Systems
layout: default
nav_order: 3
---

1. First need to run\
   `unshadow passwdfile shadowfile >unshadowed.txt`
2. Then crack with\
   `john --rules --wordlist=/usr/share/seclists/rockyou.txt unshadowed.txt`
3. Or straight use hashcat:\
   `hashcat -m 1800 -a 0 -o cracked.txt hashes.txt /usr/share/seclists/rockyou.txt -O`\
   (use `-m 500` for even old password shadow hash)