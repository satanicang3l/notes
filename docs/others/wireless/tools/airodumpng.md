---
title: Airodump-ng
parent: Wireless Attack Tools
layout: default
nav_order: 2
---

1. First need to be in monitor mode! Use airmon-ng:\
   `sudo airmon-ng start wlan0`
2. Get the wireless interface name using:\
   `iwconfig`
3. Start getting information on wireless networks for all 5ghz(a), 2.4ghz(b, g) and write it to file. This eg also includes only channel 11:\
   `sudo airodump-ng wlan0mon --band abg --write test -c 11`\
   (In this case write and channel are optional. In fact probably better to start with `sudo airodump-ng wlan0mon --band abg`)