---
title: Keepass (kdbx)
parent: Others
layout: default
nav_order: 7
---

1. First use\
   `keepass2john filename > filename.hash`
2. To crack:\
   `john --wordlist=/usr/share/seclists/rockyou.txt filename.hash`
3. Can then open kdbx with keepass software.