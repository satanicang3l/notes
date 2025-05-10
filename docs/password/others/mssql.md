---
title: MSSQL
parent: Other Passwords
layout: default
nav_order: 3
---

Can be from master.mdf or direct from DB

1. Common location:\
   `C:\Program Files\Microsoft SQL Server\MSSQL14.SQLEXPRESS\MSSQL\Backup\master.mdf`\
   `C:\Program Files\Microsoft SQL Server\MSSQL14.SQLEXPRESS\MSSQL\Binn\master.mdf`(Requires more work as cannot extract run time)
2. After getting the file, go to tools->Invoke-MDFHashes. In this folder, run `pwsh`. If not installed, get it here: https://github.com/xpn/Powershell-PostExploitation
3. Do this:\
   `Add-Type -AssemblyName ./OrcaMDF.RawCore.dll`\
   `Add-Type -AssemblyName ./OrcaMDF.Framework.dll`\
   `import-module ./Get-MDFHashes.ps1`\
   `Get-MDFHashes -mdf "/home/yengee/try/master.mdf"`
4. If you cannot see the full hash, maximize terminal and run the command again. Get the hash and crack it using John:\
   `john --format=mssql12 --wordlist=/usr/share/seclists/rockyou.txt hash.txt`
5. Alternatively hashcat (131 for SQL 2000, 132 for SQL 2005, 1731 for 2012,2014+):\
   `hashcat -m 1731 -a 0 hash.txt /usr/share/seclists/rockyou.txt`