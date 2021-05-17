# Short Cuts #
1. Make ip address a variable to reuse
    * ip=0.0.0.0
    * echo $ip
# Nmap #
1. Standard start
    * nmap -sC -sV $ip
2. Full Port Scan
    * sudo nmap -p- -sV -sS -T4 $ip
3. OS Scan
    * sudo nmap -O $ip

# HTTP #
1. gobuster dir -u $ip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x aspx,php,asp,html,txt,config,cgi 
2. nikto -host $ip -port <port>

# Brute Force #
1. SSH
   * nmap --script ssh-brute --script-args userdb=/usr/share/wordlists/nmap.lst,passdb=/usr/share/wordlists/fasttrack.txt -pT:22 $ip


# FTP #
1. nmap -v -p21 -Pn --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-syst,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221 $ip
2. nmap --script ftp-brute --script-args userdb=/usr/share/wordlists/nmap.lst,passdb=/usr/share/wordlists/fasttrack.txt -pT:21 $ip
