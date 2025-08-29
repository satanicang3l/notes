---
title: Wi-Fi Interface Command
parent: Wireless Attack
layout: default
nav_order: 15
---

1. Basic check on the card:\ 
   `iwconfig`.
2. Check country set for the card:\
   `iw reg get`
3. Set region (for eg US):\
   `sudo iw reg set US`
4. Check what your card support (check supported bands, SAE/WPA3):\
   `iw list`
5. Scan for WiFi networks (for eg using wlan0 interface). Try `sudo` if no results:\
   `iwlist wlan0 scan |  grep 'Cell\|Quality\|ESSID\|IEEE'`
6. Changing channel (for eg to 64). First need to disable the interface, then change, and bring it up again:\
   `sudo ifconfig wlan0 down`\
   `sudo iwconfig wlan0 channel 64`\
   `sudo ifconfig wlan0 up`\
   `iwlist wlan0 channel`
7. Change to monitor mode:\
   `sudo ifconfig wlan0 down`\
   `sudo iw wlan0 set monitor control`\
   `sudo ifconfig wlan0 up`
8. Change to managed/default mode:\
   `sudo ifconfig wlan0 down`\
   `sudo iwconfig wlan0 mode managed`\
   `sudo ifconfig wlan0 up`
9. Backhaul/mesh: Change to ad-hoc mode:\
   `sudo ifconfig wlan0 down`\
   `sudo iwconfig wlan0 mode ad-hoc`\
   `sudo ifconfig wlan0 up`
10. Backhaul/mesh: Change to mesh mode:\
   `sudo ifconfig wlan0 down`\
   `sudo iwconfig wlan0 mode mesh`\
   `sudo ifconfig wlan0 up`
11. Rogue AP or Evil Twin: Change to master mode. First need to create a file with the following content (change accordingly):\
    ```
    interface=wlan0
    driver=nl80211
    ssid=HTB-Hello-World
    channel=2
    hw_mode=g
    ```
    Then just run `sudo hostapd open.conf`