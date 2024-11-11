
# netexec
It is a post-exploitation and penetration testing tool that automates the assessment of large Active Directory networks. It is designed to be used to simplify and streamline the post-exploitation phase, allowing for efficient execution of various tasks on compromised systems within a network.
- `smb`: Specifies the protocol (SMB) to use.
- `ip_range`: Specifies the target IP range, for example 192.168.1.0/24.
- `-u`: Specifies the username for authentication.
- `-p`: Specifies the password for authentication.
```bash
nxc smb <ip_range> -u username -p password
# You can try to enumerate users using:
nxc smb ip --users
```


# BloodHound
It is an Active Directory (AD) reconnaissance tool that can reveal hidden relationships and identify attack paths within an AD environment.
## First time settings
- create a new neo4j console:
```bash
sudo neo4j console
```
- Connect to localhost:7474 and change the password
	- Default credentials 
		- username: neo4j 
		- password: neo4j
- Download bloodhound-python:
```bash
pip install bloodhound
```
- Add bloodhound to the path. When downloaded it's located at /home/user/.local/bin
```bash
ls /home/_user_/.local/bin
vi ~/.zshrc # Add at the end of the file export PATH=$PATH:/home/user/.local/bin
source ~/.zshrc
```
## Usage
- First, we need to collect the data
```bash
bloodhound-python -c All -u user -p password -d domain_name  -ns target_ip --zip 
```
- Remember to create your node4j console:
```bash
sudo neo4j console
```
- Upload the data
- Use the menu to see the information
- Is very useful to use the ANALYSIS tool to display visual information

## Information Analysis

The value "1" in the **Outbound Object Control** attribute indicates that a user or group has control over Active Directory objects that can generate requests or interactions with other systems, domains, or resources outside of their own authority. This control may grant them the ability to delegate privileges, modify permissions, or perform actions that affect other machines within the network, even if the attacker does not have direct access to them. This makes it a critical vector for privilege escalation and lateral movement within the infrastructure.

##### Outbound Object Control

![](bloodhound-outbound-object.png)
# NTLMRelayx.py

**ntlmrelayx.py** is a powerful tool from the Impacket toolkit used for relaying captured NTLM authentication attempts to other network services. It is particularly effective in Windows Active Directory (AD) environments, allowing attackers to gain unauthorized access to network resources by relaying credentials.

## Configuring Target List:

- Create a `targets.txt` file with the IP addresses or hostnames of the target AD servers you want to relay the captured credentials to.
```bash
192.168.1.10 
192.168.1.11
```
## Starting NTLMRelayx.py:

- Use NTLMRelayx.py to relay captured NTLM authentication attempts to the targets listed in `targets.txt`.
```bash
sudo ntlmrelayx.py -tf targets.txt -smb2support
```
- Also, NTLMRelayx.py can be configured to execute a certain command of our election after pawning one of the target hosts. 
```bash
sudo ntlmrelayx.py -tf targets.txt -smb2support -c "<command>"
```
# LDAP
## Enumeration
```bash
nmap -n -sV --script "ldap* and not brute" <IP> #Using anonymous credentials
```

