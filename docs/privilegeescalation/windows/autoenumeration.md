---
title: Auto Enumeration
parent: Windows PE
layout: default
nav_order: 1
---

Winpeas: https://github.com/carlospolop/PEASS-ng/releases/

1. use `accesschk.exe /accepteula -uws "Everyone" "C:\Program Files"` to check for weak access rights (eg check which folder or file which group everyone can write).
2. use `windows-privesc-check2.exe --dump -a` for all basic checks, or use `windows-privesc-check2.exe -h` to see what other options.
3. use `winpeas.exe quiet cmd fast` to use winpeas. If possible use `reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1` and restart cmd first.
4. use `powershell`, then `. ./PowerUp.ps1`, then `Invoke-AllChecks`.
5. use `sharpup.exe` (similar to powerup)
6. use `seatbelt.exe all` (another enum tool)