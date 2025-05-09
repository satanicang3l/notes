---
title: SMB
parent: General Usage
layout: default
nav_order: 15
---

1. Listing:\
   `smbclient -N -L IP` OR `smbclient -N -L IP -U domain/user --password=pass`\
   Accessing:\
   `smbclient -U domain/user '\\IP\ShareName'` (remove -U if no password/ID)
2. When connecting to Windows Server 2016, change the `min protocol` to `SMB2` in `/etc/samba/smb.conf`. Restart it via `sudo /etc/init.d/smbd restart` after changing.
3. Mount the share instead of accessing: `sudo mount -t cifs -o port=445 //RemoteIP/Data -o username=Administrator,password=Qwerty09! /mnt/win10_share`
4. Download all files recursively:
   `mask ""`\
   `recurse ON`\
   `prompt OFF`\
   `cd "path\to\remote\dir"`\
   `lcd "~/path/to/download/to/"`\
   `mget *`