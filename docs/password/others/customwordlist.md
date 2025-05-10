---
title: Custom Wordlist
parent: Others
layout: default
nav_order: 30
---

1. If you have a wordlists but want to transform it (for eg add numbers behind) can edit `/etc/john/john.conf` and add the following:\
   `[List.Rules:AddNumber]`\
   `# Add two numbers to the end of each password`\
   `$ [0-9]$[0-9]`\
   Subsequently run\
   `john --wordlist=before.txt --rules=AddNumber --stdout > after.txt`\
   For more info read here https://miloserdov.org/?p=5477​
2. Own custom wordlist with special pattern: `crunch minchar maxchar structure`. For eg if we want a 4-6 characters password, first 4 is uppercase letter next 4 is number can use `crunch 4 6 -t ,,,,%%%%`. If size ok then only run `crunch 4 6 -t ,,,,%%%% -o output.txt`\
   `@` lowercase\
   `,` uppercase\
   `%` numeric\
   `^` special characters including space