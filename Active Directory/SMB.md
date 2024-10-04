

# SmbClient 
It is a network protocol that allows users to communicate with remote computers and servers to use their resources or share, open, and edit files.

- `-U` access as user.
- `-N` No password.
- `-L` This option allows you to look at what services are available on a server.
```bash
smbclient -U bob //10.129.42.253/users
# You can list resources without user with this command:
smbclient -N -L //10.129.117.14/
```

# nmap scripts
Also, if after our report we observe that the machine has an SMB service we can use some useful nmap scripts to know if the target machine has a vulnerable version of SMB.
```bash
nmap -p445 --script smb-vuln-ms17-010 <target_ip>
```
After executing the nmap command if the smb service has a known vulnerability the name of the CVE will be printed.

# Smbmap
It is designed to enumerate and interact with shared files and another resources, providing information about their accessibility, permissions, and potential vulnerabilities.
- `-H`: Specifies the target IP address (replace "192.168.1.100" with the actual IP).
- `-u`: Specifies the username for authentication.
- `-p`: Specifies the password for authentication.
```bash
smbmap -H ip -u username -p password
```

## Netexec (Crackmapexec)
CME can enumerate users and their privileges on Windows systems using the SMB protocol.
### Basic Usage
```bash
crackmapexec smb <ip> -u 'username' -p 'password'
```

### --rid-brute
This option enables the RID (Relative Identifier) brute-force enumeration feature. It tells CrackMapExec to try various RIDs to enumerate user accounts and retrieve their security identifiers (SIDs). This is useful for discovering valid usernames on the target system, especially if the `guest` account successfully authenticates.
```bash
crackmapexec smb 10.10.11.35 -u 'guest' -p '' --rid-brute
```