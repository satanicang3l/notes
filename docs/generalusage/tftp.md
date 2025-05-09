---
title: TFTP
parent: General Usage
layout: default
nav_order: 14
---

1. To enumerate: `nmap -n -Pn -sU -p69 -sV --script tftp-enum <IP>`
2. Cannot list folder, so need to use things like `get windows\system32\license.rtf` (or similar)
3. If want to upload, use `binary`, then `put xx.exe`
4. If transferring text file can use the default mode. If not need to use `mode binary` to download exe files. (default is `mode ascii`)

## TFTPY
The actual TFTP sucks.. Use this better..

1. (DONE) In case not installed, go python2 folder, `pipenv shell`, then `python -m pip install tftpy.`
2. Go python2 script folder, `pipenv shell`. Then execute `python`.
3. Next (change IP, path, port accordingly):
   `import tftpy`\
   `client = tftpy.TftpClient('10.11.1.111', 69)`\
   `client.download('\Program Files\Microsoft SQL Server\MSSQL14.SQLEXPRESS\MSSQL\Backup\master.mdf', 'master.mdf')`
4. Can upload as well in a similar manner: `client.upload(input=srcfilepath, filename=destfilepath)`