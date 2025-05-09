---
title: SSH / SCP
parent: General Usage
layout: default
nav_order: 30
---

Copy the pub keys to `~/.ssh/authorized_keys` to gain access to that server

To fix the permission for id_rsa, use `sudo chmod 600 ~/.ssh/id_rsa`

`scp -P port [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2`\
(if copy to localhost no need put localhost, just use full path like /home/xxx/yyy)