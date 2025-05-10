---
title: Manual Enumeration
parent: Linux PE
layout: default
nav_order: 3
---

1. use `id` to find out about user and group info. `cat /etc/passwd` to find out about other users.
2. `hostname` to find out pc name. `cat /etc/issue` and `uname -a` will both display the OS info.
3. `ps axu` to get info on running processes. `ifconfig a` to show IP config info. `route`/`routel` to show routing table. `netstat -anp` to show active connections.
4. to see firewall usually need to have root (`iptables`). However can check `cat /etc/iptables` also to see if got any info there.
5. use `ls -lah /etc/cron*` to find out interval scheduled jobs (hourly, weekly etc). `cat /etc/crontab` to find out custom tasks.
6. use `dpkg -l`, `apt list --installed` or `rpm -qa` to list installed packages.
7. `find / -writable -type d 2>/dev/null` to find out folder with write permission (use `f` for file) by current user.
8. use both `mount` and `cat /etc/fstab` to find out info on mounted drive. `/bin/lsblk` to see all available drives.
9. use `lsmod` to see list of modules, then `/sbin/modinfo modname` to get specific info.
10. use `find / -perm -u=s -type f 2>/dev/null` to find file with SUID bit.
11. Check for common backup file location, such as:\
    `ls -la /`\
    `ls -la /tmp`\
    `ls -la /var/backups/`\
    `ls -la /home/user/`