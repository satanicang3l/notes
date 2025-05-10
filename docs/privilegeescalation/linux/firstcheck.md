---
title: First Check
parent: Linux
layout: default
nav_order: 2
---

1. Sudo can run:\
   `sudo -l`
2. Find file with SUID:\
   `find / -perm -u=s -type f 2>/dev/null`\
   Folder and files:\
   `find / -perm /u=s,g=s 2>/dev/null`
3. GTFOBins for further exploit:\
   https://gtfobins.github.io/