---
title: 113 (ident)
parent: Ports
nav_order: 999
---

If ident is open (usually port 113), can try to enum the username for any service.

Use the following (replace port with the port number of service you want to know, NOT 113):\
`ident-user-enum IP PORT`

Based on this username go to bruteforce username/password for eg in ssh.