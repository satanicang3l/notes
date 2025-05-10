---
title: Installed Application
parent: Method (Windows)
layout: default
nav_order: 8
---

IMPORTANT, use 32 bit shell for 32 bit, and 64 bit shell for 64 bit exploit! Check Program Files or Program Files(x86) if not sure!

1. Get all running prorgrams: `tasklist /v`
2. Seatbelt for nonstandard process: `seatbelt.exe NonstandardProcesses`
3. winpeas to check: `winpeas.exe quiet processinfo`
4. Identify the version, eg run with `/?` or `/h`, or check the config or text file in the directory.
5. Search for an exploit (`searchsploit xx`)