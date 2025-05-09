---
title: PATH
parent: General Usage
layout: default
nav_order: 24
---

## Linux
1. Prepend: `export PATH=/some/new/path:$PATH`
2. Append: `export PATH=$PATH:/some/new/path`
3. Quick way to add default PATH:\
   `export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`

## Windows
Add default PATH:\
`path=%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;%SystemRoot%\System32\WindowsPowerShell\v1.0;`