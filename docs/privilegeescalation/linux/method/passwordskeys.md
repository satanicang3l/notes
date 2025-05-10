---
title: Passwords and Keys
parent: Method
layout: default
nav_order: 5
---

## History File
1. use to access history: `cat ~/.*history | less`
2. `su` to the user using password discovered

## Config files
1. Sometimes config file can hint to hidden plaintext password.
2. `find . -iname '*config*'` in the directory you think might have.
3. For example ovpn config file might contain auth-user-pass option and a file name.
4. This file will contain plaintext credentials. Can then su.

## SSH Keys
1. Search for SSH private keys that are not configured properly, for eg in / directory:\
   `ls -l /.ssh`
2. Copy to Kali and change permission:\
   `chmod 600 root_key`
3. Connect using key:\
   `ssh -i root_key root@IP`