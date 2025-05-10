---
title: Manual Enumeration
parent: Windows PE
layout: default
nav_order: 2
---

1. find out `whoami`, then `net user username` to find out more info. `net user` only to find out about other user. (`echo %userprofile%` also can)
2. `hostname` to find out pc name. `systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"` to find out more about OS version.
3. `tasklist /SVC` to get running processes related to service. `ipconfig /all` to display IP config info, and `route print` to show all routing tables. `netstat -ano` to display active network connections.
4. `netsh advfirewall show currentprofile` to check if firewall on. `netsh advfirewall firewall show rule name=all` to check on all firewall rules.
5. `schtasks /query /fo LIST /v` to show all scheduled tasks.
6. `wmic product get name, version, vendor` to get installed by windows installer software. `wmic qfe get Caption, Description, HotFixID, InstalledOn` to list installed update.
7. accesschck preferred (auto), if not can use `powershell` then `Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString -match "Everyone\sAllow\s\sModify"}` for modifiable file for group everyone.
8. `mountvol` to check all volumes, mounted or unmounted.
9. first `powershell`, then `driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object ‘Display Name’, ‘Start Mode’, Path` to get a list of drivers and kernel modules. Finally use `Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like "*VMware*"}` to get the specific info (in this case for vmware).
10. if either of these true:\
    `reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`\
    `reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer` then can craft MSI file which will elevate as admin.