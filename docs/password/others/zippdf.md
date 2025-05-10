---
title: VNC
parent: Other Passwords
layout: default
nav_order: 6
---

For PDF, ZIP or RAR:\
`pdf2john filename > filename.hash`\
`zip2john filename > filename.hash`\
`rar2john filename > filename.hash`

Then to crack run\
`john --wordlist=/usr/share/seclists/rockyou.txt filename.hash`