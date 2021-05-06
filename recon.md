# Short Cuts #
1. Make ip address a variable to reuse
    * ip=0.0.0.0
    * echo $ip
# Nmap #
1. Standard start
    * nmap -sC -sV $ip
2. Full Port Scan
    * nmap -p- -sV -sS -T4 $ip
3. OS Scan
    * nmap -O $ip
