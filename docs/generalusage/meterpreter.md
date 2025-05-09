---
title: Meterpreter
parent: General Usage
layout: default
nav_order: 5
---

1. To auto migrate to stable shell when listening connection, in multi/handler. use:
   `set AutoRunScript post/windows/manage/migrate`
2. To automatically run something in Linux after receiving connection, use `set AutoRunScript /home/yengee/test`\
(very important to have no extension).\
In this test file, put in your commands (for example `whoami`, `id `etc)