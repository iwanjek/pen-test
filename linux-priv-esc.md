# Restricted Shell #
  1. https://www.hacknos.com/rbash-escape-rbash-restricted-shell-escape/
# What Can We Do #
  1. whoami
  2. sudo -l

# Check Scheduled Tasks #
  1. crontab -l
  2. less /etc/crontab

# Check what processes are running root #
 use ps -aux | grep root

# SUID Checker #
  1. find / -perm -u=s -type f 2>/dev/null

# SUID Execute #
Bash, Cat, cp, echo, find, Less, More, Nano, Nmap, Vim and etc

# Unshadow #
sudo unshadow passwd.bak shadow.bak > pwd.txt
