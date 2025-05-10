---
title: RINETD
parent: Pivot
layout: default
nav_order: 9
---

1. Install RINETD:\
   `sudo apt update && sudo apt install rinetd`
2. Edit the file /etc/rinetd.conf. Like for example to bind port 80 to Google can use (bind connect):\
   `0.0.0.0 80 216.58.207.142 80`
3. Restart the service with\
   `sudo service rinetd restart`\
   (`ss -antp | grep "80"`) to confirm.
4. This way everyone that connects to our IP port 80 will be redirected to 216.58.207.142 port 80.