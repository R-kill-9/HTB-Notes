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