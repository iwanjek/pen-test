# Short Cuts #
1. Make ip address a variable to reuse
    * ip=0.0.0.0
    * echo $ip
# Nmap #
Always neumerate all ports especially services that are unknown or tcpwrapped
1. Standard start
    * nmap -sC -sV $ip -Pn
2. Full Port Scan
    * sudo nmap -p- -sV -sS -T4 $ip -Pn
    * nmap -vv --reason -Pn -A --osscan-gues --version-all -p- $ip 
3. OS Scan
    * sudo nmap -O $ip

# HTTP #
0. If webrowser cannot connect to domain name (i.e. ip address turn into domain name but can't connect ) add the domain name to your etc hosts file
1. If you get a smb sharename it could be the directory of a wordpress
2. gobuster dir -u $ip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x aspx,php,asp,html,txt,config,cgi      (use -b to exclude status codes)
3. nikto -host $ip -port <port>
4. curl -d "" -X POST https://example.com/ (Sometimes webrowsers will allow POST request when a GET is not working -d "" adds content filler of nothing in case content required)

# SNMP #
1. snmp-check $ip
   look for unusual processes


# Brute Force #
1. SSH
   * nmap --script ssh-brute --script-args userdb=/usr/share/wordlists/nmap.lst,passdb=/usr/share/wordlists/fasttrack.txt -pT:22 $ip
2. For all passwords check to see if it is a hash or base64 or plain text
3. pdfcrack -f filname.pdf -w rockyou.txt


# FTP #
   try anonymous/anonymous or admin/admin
1. nmap -v -p21 -Pn --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-syst,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221 $ip
2. nmap --script ftp-brute --script-args userdb=/usr/share/wordlists/nmap.lst,passdb=/usr/share/wordlists/fasttrack.txt -pT:21 $ip

 # SMTP #
  1. telnet $ip 25
   
 # REDIS 6379 #
1. https://book.hacktricks.xyz/pentesting/6379-pentesting-redis
2. If you have the ability to upload a file then you can upload a redis module that give code execution
   
  # ICR #
   1. https://book.hacktricks.xyz/pentesting/pentesting-irc
   2. Use hexchat to join chatroom. Readd the clues from messages.
 
