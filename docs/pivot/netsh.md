---
title: NetSH
parent: Pivot
layout: default
nav_order: 6
---

For Windows machine (useful when have another network segment).
Need to have SYSTEM access.
The Service "IP Helper" must be running, and IPv6 support must be enabled.

1. Use the following on victim machine:\
   `netsh interface portproxy add v4tov4 listenport=VICTIMLISTENPORT listenaddress=VICTIMIP connectport=OTHERHOSTPORT connectaddress=OTHERHOSTIP`
2. Also need to add it through firewall so that can connect:\
   `netsh advfirewall firewall add rule name="forward_port_rule" protocol=TCP dir=in localip=VICTIMIP localport=VICTIMLISTENPORT action=allow`
3. Can access via the victim IP and victim listen port now.