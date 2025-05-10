---
title: Insecure GUI App
parent: Method (Windows)
layout: default
nav_order: 5
---

1. If you can run some apps with admin rights (only way to test is to open and run `tasklist /V | findstr proccessname.exe` and check manually)
2. Find a place where you can open file / access file in the GUI, and input `file://c:/windows/system32/cmd.exe`