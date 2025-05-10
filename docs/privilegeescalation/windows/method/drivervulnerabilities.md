---
title: Driver Vulnerabilities
parent: Method (Windows)
layout: default
nav_order: 11
---

1. First is to get detailed info of the OS: `systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"`
2. Next to get all installed driver: `driverquery /v`. Prioritise 3rd party drivers as they are usually easier (stopped also can use)
3. Use `searchsploit drivername` and see if there is any vulnerable driver.
4. To verify driver version installed, either browse to `C:\Windows\System32\Drivers` or `C:\Program Files\Name` and find a *.inf file. This will usually tell you the driver version.
5. Compile the exploit if needed, transfer to the victim and run it to see if it works.