---
title: HTTPTunnel
parent: Pivot
layout: default
nav_order: 7
---

If all other ports blocked(SSH eg), only can HTTP

1. First connect to the second victim IP. On the first victim, bind our port 8888 to a third party IP 192.168.1.110:3389 using a student account we created on the first victim post exploit:\
   `ssh -L 0.0.0.0:8888:192.168.1.110:3389 student@127.0.0.1`
2. Next on first machine we need to listen on port 1234 and forward to port 8888 (which will be redirected to 192.168.1.110:3389):\
   `hts --forward-port localhost:8888 1234`
3. Finally on our Kali we need to listen on port 8080 and forward it via HTTP Tunnel to first victim port 1234:\
   `htc --forward-port 8080 10.11.0.128:1234`
4. Now we can use Kali to connect to local port 8080 to access 192.168.1.110:3389