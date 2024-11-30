**Nmap (Network Mapper)**  allows users to scan networks, identify hosts, and determine open ports, services, and operating systems running on devices.
```bash
nmap  -sS -sCV -p21 <ip_address>
```

- `-sV` Shows the version of the service running on each port.
- `-sC` Uses additional scripts to gather more information.
- `-sS` Stealth scan.
- `-sn` Is used for a ping scan, where Nmap identifies which hosts are alive (up) in a network without performing a port scan on those hosts.
- `-sU` Scans the UDP ports. 
- `-p-` Scans all ports. 
- `-Pn` Skip recognition phase.
- `-O` Determines the operating system of the target.
- `-p <port>` Scans only the specified port number. 
- `-vvv` Increase verbosity.
- `--open` Only displays open ports.
- `--min-rate` Specifies the minimum number of packets Nmap should send per second; increasing this number speeds up the scan. 
- `-T[0...5]` Sets the timing template, which controls the speed and aggressiveness of the scan.
- `-oN,-oG,-oX` Saves the scan results in a human-readable plain text format (-oN), in XML format (-oX) or in grepable format (-oG).

## nmap scripts
**nmap** has the option of checking if there are some known vulnerabilities for the services versions that are being used at the machine. We just need to specify the port and the target ip.
```bash
nmap -p<port> --script vuln <target_ip>
```
