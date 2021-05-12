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
    * nmap -O $ip

# HTTP #
1. gobuster dir -u $ip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x aspx,php,asp,html,txt,config,cgi 
