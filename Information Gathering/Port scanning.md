# nmap
- `-sV` shows the version of the service running on each port.
- `-sC` uses additional scripts to gather more information.
- `-sS` stealth scan.
- `-p-` scans all ports. 
-  `-Pn-` Skip recognition phase.
- `-p <port>` scans only the specified port number. 
-  `--open` only displays open ports.
- `--min-rate` Specifies the minimum number of packets Nmap should send per second; increasing this number speeds up the scan. 
```bash
nmap  -sS -sC -sV -p21 10.129.42.253
```
## nmap scripts
**nmap** has the option of checking if there are some known vulnerabilities for the services versions that are being used at the machine. We just need to specify the port and the target ip.
```bash
nmap -p<port> --script vuln <target_ip>
```
