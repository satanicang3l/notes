---
title: HTPASSWD
parent: Web Passwords
layout: default
nav_order: 5
---

Sample: `$apr1$oRfRsc/K$UpYpplHDlaemqseM39Ugg0`

1. hashcat:\
   `hashcat -m 1600 -a 0 hash.txt /usr/share/seclists/rockyou.txt`