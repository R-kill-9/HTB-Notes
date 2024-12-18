Network Basic Input/Output System (NetBIOS) is a protocol that allows applications on different computers to communicate within a LAN. It is used for file sharing, printer sharing, and identifying devices on a network.

**Key Ports for NetBIOS**

- **UDP 137**: NetBIOS Name Service (NBNS) - Name resolution.
- **UDP 138**: NetBIOS Datagram Service - Communication between devices.
- **TCP 139**: NetBIOS Session Service - File sharing and resource access.

## Enumeration

**nmap**: Scans for NetBIOS services and shared resources.

```bash
nmap -sU -p 137 <IP>
nmap -sS -p 139,445 <IP>
```

**nbtscan**: Quickly enumerates NetBIOS information on a network.

```bash
nbtscan <IP_range>
```