---
title: Powershell
parent: General Usage
layout: default
nav_order: 4
---

1. Disable execution policy:\
   `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted`\
   (Use `-Scope Process` if access denied)
2. Can put the scripts in the folder below:\
   `System32\WindowsPowerShell\v1.0\Modules`, and then run PS:\
   `Import-Module xxx`\
   (can type full path also if dowan put there)
3. Can also use dot: `. ./xx.ps1`
4. If powershell unresponsive when go in:\
   `powershell.exe Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted`

## Powershell Remote Command

Need admin access.

Enable powershell remoting on current machine:\
`Enable-PSRemoting`

Once you have the service: Using Powershell,\
`Enter-PSSession computername`