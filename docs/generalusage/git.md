---
title: Git
parent: General Usage
layout: default
nav_order: 19
---

1. Use `git clone https://github.com/x.git` to clone the entire folder. After that `cd` into that folder. Then use `pyenv local 3.10.6`, `pipenv install` before doing python related things.
2. For maven related, use `maven package` in the application directory.
3. In the git directory, run `git log` to read the changelog.

## Pushing Git Changes
1. Clone the git first (change git-server to whatever git it is):\
   `git clone file:///git-server/`
2. First set up the identity (change to the username and hostname on the running PC):\
   `git config --global user.name "user"`\
   `git config --global user.email "user@hostname.(none)"`
3. Make whatever changes you want to change. If you change something executable, remember to `chmod +x` it.
4. Add and commit the change:\
   `git add -A`\
   `git commit -m "pwn"`
5. Push the change to server:\
   `git push origin master`