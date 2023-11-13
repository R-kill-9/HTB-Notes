**Active Directory** (AD) is a directory service developed by Microsoft for managing and organizing information about network resources, such as computers, users, and devices, within a Windows network environment. It serves as a centralized database that enables administrators to efficiently and securely manage and authenticate users, computers, and other network elements.

## Samba/SMB Port <a name='smb'></a>

### SmbClient 
It is a network protocol that allows users to communicate with remote computers and servers to use their resources or share, open, and edit files.

- `-U` access as user.
- `-N` No password.
- `-L` This option allows you to look at what services are available on a server.
```bash
smbclient -U bob \\\\10.129.42.253\\users
# You can list resources without user with this command:
smbclient -N -L \\\\10.129.117.14\\
```

### nmap scripts
Also, if after our report we observe that the machine has an SMB service we can use some useful nmap scripts to know if the target machine has a vulnerable version of SMB.
```bash
nmap -p445 --script smb-vuln-ms17-010 <target_ip>
```
After executing the nmap command if the smb service has a known vulnerability the name of the CVE will be printed.

### Smbmap
It is designed to enumerate and interact with shared files and another resources, providing information about their accessibility, permissions, and potential vulnerabilities.
- `-H`: Specifies the target IP address (replace "192.168.1.100" with the actual IP).
- `-u`: Specifies the username for authentication.
- `-p`: Specifies the password for authentication.
```bash
smbmap -H ip -u username -p password
```

## Crackmapexec
It is a post-exploitation and penetration testing tool that automates the assessment of large Active Directory networks. It is designed to be used to simplify and streamline the post-exploitation phase, allowing for efficient execution of various tasks on compromised systems within a network.
- `smb`: Specifies the protocol (SMB) to use.
- `ip_range`: Specifies the target IP range, for example 192.168.1.0/24.
- `-u`: Specifies the username for authentication.
- `-p`: Specifies the password for authentication.
```bash
crackmapexec smb ip_range -u username -p password
```