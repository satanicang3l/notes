---
title: Netcat / SMTP (Write)
parent: General Usage
layout: default
nav_order: 8
---

1. To send email (usually port 25, -C is to send a complete line feed to imitate telnet):\
   `nc -C IP PORT`
2. Then use the following line by line:\
   `EHLO domainname (or HELO)`\
   `MAIL FROM: a@email.com`\
   `RCPT TO: recepient@email.com`\
   `DATA`
3. From here can enter the email content, until a single dot. Usually can put something like below:\
   `From: bar@example.org`\
   `To: foo@example.com`\
   `Subject: Test`\
   `Date: Thu, 20 Dec 2012 12:00:00 +0000`\
   ` `\
   `Content`\
   `.`\
   ` `\
   `QUIT` to end