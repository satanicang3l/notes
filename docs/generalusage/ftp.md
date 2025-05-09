---
title: FTP
parent: General Usage
layout: default
nav_order: 12
---

1. `ftp ftp://user:password@host:port`, then use `get xx.txt` to download the content
2. To use binary mode, just type `binary`. Set active mode: `passive off`. Then use `put /home/yengee/a.txt b.txt` to upload file.
3. When connecting can use `-p` to force passive mode.