# Did you revert the box? Never trust that the box is working properly #
# Recon #
1. Did you scans:
  a. Full scan (hidden Ports)
  b. UDP scan
2. Searchsploit all services
3. Try default creds for all services admin/admin etc.
4. Go to a webpage for any name you found. For instance if there is a "sushi" directory/file in ftp go to http:$ip/sushi. Common trick to fool dirbuster
5. Did you gobuster each http?

# Foothold #
1. Try all different ports for reverse shell. Somemtimes a port is open but only outbound.
2. Try all different reverse shells
3. If web requests GET doesn't work trying curl POST
4. Watch out your URL encoding isnt getting interfered. Like turning spaces to + instead of %20
5. Look for weird stuff in brupsuite like what level of access something might have? Is something base64 encoded?


# Priv Esc #
1. What files do I have access to?
2. What groups?
3. What can sudo do?
4. Any cron jobs?
5. Any strange programs in program files or strange scripts somewhere?
6. What is the path? Does it call something I can hijack?
7. Are your calling /bin when it should be /sbin or another path issue?
8. Can you overwite an important file?
9. Can you move a file to replace it with a reverse shell?



# Password Breaking #
1. You can use hashcat to identify hash patterns
2. Always assume names you have already found
3. Base64 is common
4. pdfcrack -w (using a wordlist) powerful tool

