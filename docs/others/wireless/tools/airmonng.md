---
title: Airmon-ng
parent: Wireless Attack Tools
layout: default
nav_order: 1
---

1. Display interface and chipset information:\
   `sudo airmon-ng`
2. Go into monitor mode:\
   `sudo airmon-ng start wlan0`\
   `iwconfig` to check if it works
3. Check interfering process:\
   `sudo airmon-ng check`
4. Kill the interfering processes (dont simply kill unless really got problem):\
   `sudo airmon-ng check kill`
5. Start monitor mode on specific channel:\
   `sudo airmon-ng start wlan0 11`
6. Stop monitor mode:\
   `sudo airmon-ng stop wlan0mon`