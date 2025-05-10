---
title: IP Namespace (Segregate VPN in case Routing Conflict)
parent: Pivot
layout: default
nav_order: 8
---

1. Create a new namespace:\
   `sudo ip netns add openvpn_namespace`
   `sudo ip netns`
2. Attach whatever interface you want to this namespace (eg in this case tun0):\
   `sudo ip link set tun0 netns openvpn_namespace`\
   `sudo ip netns exec openvpn_namespace ip link set tun0 up`\
   `sudo ip netns exec openvpn_namespace ip link`\
   `sudo ip netns exec openvpn_namespace ip addr`
3. Now need to manually assign your IP address to the linked namespace (eg below 10.8.0.2 on tun0 is assigned when connected to the VPN):\
   `sudo ip netns exec openvpn_namespace ip addr add 10.8.0.2/24 dev tun0`\
   `sudo ip netns exec openvpn_namespace ip addr`
4. After that add the routing information manually (example below 10.200.23.0/24 is routed through 10.8.0.1):\
   `sudo ip netns exec openvpn_namespace ip route`\
   `sudo ip netns exec openvpn_namespace ip route add 10.200.23.0/24 via 10.8.0.1 dev tun0`\
   `sudo ip netns exec openvpn_namespace ip route`
5. When executing command (for example connect to RDP just use the namespace):\
   `sudo ip netns exec openvpn_namespace xfreerdp /u:Mbouctroupeau /d:. /p:aisle-armament-PUDDLE /v:10.200.0.192`