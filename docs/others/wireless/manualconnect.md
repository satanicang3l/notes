---
title: Manual Connection
parent: Wireless Attack
layout: default
nav_order: 14
---

## Easiest method

1. To get the wireless interface:\
   `iwconfig`
2. (Optional) If it is not up enable it:\
   `sudo ifconfig wlan0 up`
3. Scan for SSID:\
   `sudo iwlist wlan0 scan | grep ESSID`
4. Create wpa_supplicant file (can wrap ESSID in double quotes if got space). If passphrase got special character just run `wpa_passphrase your-ESSID` and enter password manually:\
   `wpa_passphrase your-ESSID your-passphrase | tee test_network.conf`
5. Connect to it:\
   `sudo wpa_supplicant -c test_network.conf -i wlan0`
6. Confirm it is working with:\
   `iwconfig`
7. End the process and connect it in background:\
   `sudo wpa_supplicant -B -c test_network.conf -i wlan0`
8. Obtain D:\
   `sudo dhclient wlan0`


## Open Network

```
network={
  ssid="hotel_wifi"
  scan_ssid=1
}
```

## WEP

```
network={
    ssid="Your_WEP_SSID"
    key_mgmt=NONE
    wep_key0="yourwepkey"
}
```

## WPA/WPA2

Optional to add `pairwise=CCMP` or `pairwise=TKIP`

```
network={
  ssid="home_network"
  scan_ssid=1
  psk="correct battery horse staple"
  key_mgmt=WPA-PSK
}
```