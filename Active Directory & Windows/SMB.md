
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

To **list the contents of a specific directory** inside a shared resource on the server:

1. Connect to the shared resource using `smbclient`.
2. Once inside, use the `ls` command to view the contents of the current directory.

```bash
smbclient //10.129.42.253/users -U bob
smb: \> ls
```

To download all content from a shared resource using `smbclient`, you can use the `mget *` command, which downloads all files in the current directory.

```bash
smb: \> mget *
```

To download all files and directories you need to execute these commands:

```bash
# Enable recursive download
smb: \> recurse ON
# Turn off interactive prompts for each file
smb: \> prompt OFF
# Download all files and folders
smb: \> mget *
```

# Eternal Blue
**Eternal Blue** is a critical vulnerability in the SMBv1 protocol  on Windows systems, specifically identified as **MS17-010** or **CVE-2017-0144**. This exploit allows attackers to execute remote code on unpatched systems, granting full access to compromised machines without needing authentication.
#### **Affected Systems**

- **Windows Server** versions:
    - **Windows Server 2003**
    - **Windows Server 2008 / 2008 R2**
    - **Windows Server 2012 / 2012 R2**
    - **Windows Server 2016** (unpatched)
    - **Windows Server 2019** (if SMBv1 is manually enabled and unpatched)
- **Windows OS Versions**:
    
    - **Windows XP**
    - **Windows Vista**
    - **Windows 7**
    - **Windows 8 / 8.1**
    - **Windows 10** (unpatched)
    
_Note_: Systems with SMBv1 disabled or patched against MS17-010 are generally protected from EternalBlue.

This nmap script allows you to know if the target machine is vulnerable to `Eternal Blue`.

```bash
nmap -p445 --script smb-vuln-ms17-010 <target_ip>
```

After executing the nmap command if the SMB service is vulnerable the associated CVE will be printed.

After validating the existance of the vulnerability, it can be exploited using `Metasploit`.

```bash
msfconsole
search eternalblue
use 0
```

# Smbmap
It is designed to enumerate and interact with shared files and another resources, providing information about their accessibility, permissions, and potential vulnerabilities.
- `-H`: Specifies the target IP address (replace "192.168.1.100" with the actual IP).
- `-u`: Specifies the username for authentication.
- `-p`: Specifies the password for authentication.
```bash
smbmap -H ip -u username -p password
```

## Netexec (Crackmapexec)
CME can enumerate users and their privileges on Windows systems using different type of protocols.
### Basic Usage
```bash
netexec smb <ip> -u 'username' -p 'password'
```

Once you have successfully authenticated to the SMB service on the target machine using **CrackMapExec** (CME), there are several actions you can take to further assess the security of the system or gather more information. Here’s a list of potential next steps:

- Enumerate Shares

```bash
netexec smb <ip> -u 'username' -p 'password' --shares
```

- Access shared files

```bash
netexec smb <ip> -u 'username' -p 'password' --get 'share_name/file_path'
```

- Access shared files

```bash
netexec smb <ip> -u 'username' -p 'password' --get 'share_name/file_path'
```

- Execute Commands Remotely

```bash
netexec smb <ip> -u 'username' -p 'password' --exec -c 'command'
```


- Check User and Group Information

```bash
netexec smb <ip> -u 'username' -p 'password'--users
```


- Password Dumping

```bash
netexec smb <ip> -u 'username' -p 'password'--ntds
```

### --rid-brute
This option enables the RID (Relative Identifier) brute-force enumeration feature. It tells CrackMapExec to try various RIDs to enumerate user accounts and retrieve their security identifiers (SIDs). This is useful for discovering valid usernames on the target system, especially if the `guest` account successfully authenticates.
```bash
crackmapexec smb 10.10.11.35 -u 'guest' -p '' --rid-brute
```