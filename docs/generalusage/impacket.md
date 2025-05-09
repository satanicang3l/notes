---
title: Impacket
parent: General Usage
layout: default
nav_order: 11
---

## Password available:
1. PSExec (will be using nt authority/system if admin):`impacket-psexec 'domain/user:password'@IP`
2. SMBExec: `impacket-smbexec "Domain/User:pass"@IP`\
   (local auth put a `.` for domain)
3. WMIExec: `impacket-wmiexec domain/user:pass@IP`\
   (local auth put a `.` for domain)
4. Evil-winrm: `evil-winrm -i targetIP -u user -p pass`

## Hash available:
1. PSExec: `impacket-psexec -hashes aaa:bbb "Domain/User"@IP`\
   (local auth put a `.` for domain)
2. SMBExec: `impacket-smbexec -hashes aaa:bbb "Domain/User"@IP`\
   (local auth put a `.` for domain)
3. WMIExec: `impacket-wmiexec -hashes aaa:bbb "Domain/User"@IP`\
   (local auth put a `.` for domain)
4. Evil-winrm (not really but put here): `evil-winrm -u user -H hash -i targetIP`
5. If no LM hashes, can either put 32 0s (`00000000000000000000000000000000`) or just use `:NThash`.

If everything fails, use `runas /env /profile /user:domain\user "command to run"`