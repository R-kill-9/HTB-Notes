

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

# netexec
It is a post-exploitation and penetration testing tool that automates the assessment of large Active Directory networks. It is designed to be used to simplify and streamline the post-exploitation phase, allowing for efficient execution of various tasks on compromised systems within a network.
- `smb`: Specifies the protocol (SMB) to use.
- `ip_range`: Specifies the target IP range, for example 192.168.1.0/24.
- `-u`: Specifies the username for authentication.
- `-p`: Specifies the password for authentication.
```bash
nxc smb ip_range -u username -p password
# You can try to enumerate users using:
nxc smb ip --users
```

# LDAP
## Enumeration
```bash
nmap -n -sV --script "ldap* and not brute" <IP> #Using anonymous credentials
```


# BloodHound
It is an Active Directory (AD) reconnaissance tool that can reveal hidden relationships and identify attack paths within an AD environment.
## First time settings
- create a new neo4j console:
```bash
sudo neo4j console
```
- Connect to localhost:7474 and change the password
	- Default credentials username: neo4j password: neo4j
- Download bloodhound-python:
```bash
pip install bloodhound
```
- Add bloodhound to the path
	- When downloaded it's located at /home/_user_/.local/bin
```bash
ls /home/_user_/.local/bin
vi ~/.zshrc # Add at the end of the file export PATH=$PATH:/home/user/.local/bin
source ~/.zshrc
```
## Usage
- First, we need to collect the data
```bash
bloodhound-python -dns-tcp -ns target_ip -d domain_name -u user -p password
```
- Remember to create your node4j console:
```bash
sudo neo4j console
```
- Upload the data
- Use the menu to see the information
- Is very useful to use the ANALYSIS tool to display visual information

# Kerberoasting
It is a method used to extract and crack service account passwords that utilize Kerberos authentication within a Windows Active Directory environment. This attack targets accounts with Kerberos Service Principal Names (SPNs) set, allowing attackers to request encrypted service tickets from the domain controller.
- One method that can be used is using 'impacket-GetUserSPNs'. If we have a user with a username ended in *TGS* that means that is part of a TICKET GRANTING SERVICE. We can use this to ask a ticket to the Domain Controller.
```bash
impacket-GetUserSPNs -request -dc-ip target_ip domain_name/user
```