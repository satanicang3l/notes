---
title: Git
parent: Recon
nav_order: 3
---

- Can first check the `http://x.x.x.x/.git/config` and `http://x.x.x.x/.git/HEAD` for git information leak.
- From the HEAD file, if it is referring to refs/heads/master, you can navigate to `.git/refs/heads/master`
- This will provide you with a file hash. If the hash is aabbbbbbbb, browse to `.git/objects/aa/bbbbbbbb` (first 2 characters being the folder)
- After downloading this file, use gzip to uncompress this file:
  1. `printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" |cat - bbbbbbbb |gzip -cd -q`
  2. `ruby -rzlib -e 'print Zlib::Inflate.new.inflate(STDIN.read)' < bbbbbbbb`
- There should be a new commit for you to download from this new file, browse and download the `.git/objects/yy/ccccccccc` (first 2 characters being the folder)
- (Optional) On this new one, use strings to read the content `ruby -rzlib -e 'print Zlib::Inflate.new.inflate(STDIN.read)' < ccccccccc | strings -a`
- Create our own local repo:
  1. `mkdir /tmp/hack`
  2. `cd /tmp/hack`
  3. `git init`
- Copy our files into it:
  1. `mkdir -p .git/objects/aa .git/objects/yy`
  2. `cp /tmp/bbbbbbbb /tmp/hack/.git/objects/aa/`
  3. `cp /tmp/ccccccccc /tmp/hack/.git/objects/yy/`
- Can continue to download all the files (using the file hash). Subsequently can use the command (need to combine the first 2 characters as well, don't separate):
  git cat-file -p yyccccccccc
- After you clone a project (`git clone https://github.com/xx/yy`), cd to it and use `git log` to see the history of what has been changed.
- `tig` is a very useful way to compare the files in the same directory. Just type `tig`(need to install if don't have it), then press enter on the file, then can scroll up and down to see the differences.
