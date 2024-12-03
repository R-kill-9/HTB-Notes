**Firewall Detection & IDS Evasion** involve techniques used during network reconnaissance or penetration testing to bypass security measures like firewalls and Intrusion Detection Systems (IDS).

You can use **Nmap** to detect the presence of a firewall or Intrusion Detection System (IDS) by analyzing responses and timing patterns during a scan. 

## Detection
#### Check for Filtered Ports
Run a basic scan to check the state of ports:

```bash
nmap -p <port-range> <target>
```

If many ports are marked as `filtered`, it may indicate a firewall is blocking traffic.

#### Use ACK Scans (-sA)
ACK scans are useful to determine if a firewall is present by analyzing how it handles packets:
```bash
nmap -sA -p <port-range> <target>
```
- **Unfiltered**: A RST response means there is no filtering.
- **Filtered**: No response or an ICMP "Destination Unreachable" message suggests a firewall.

## Evasion
#### -f (Fragment Packets)

The `-f` flag enables packet fragmentation, breaking the scan packets into smaller fragments. This can help evade basic firewalls or intrusion detection systems (IDS) that struggle to reassemble fragmented packets.

To bypass simple packet filtering or evade detection by IDS.

```bash
nmap -f <target>
```

#### -S (Spoof Source Address)

The `-S` flag allows you to specify a fake source IP address for the scan, making it appear as if the packets originated from another machine.

Often combined with decoys or proxies to avoid detection.  

**Note:** Replies to the spoofed IP won't reach you unless it's under your control, limiting the effectiveness of certain scan types.

```bash
nmap -S 192.168.1.1 <target>
```

#### -ttl (Time-to-Live)

The `-ttl` flag sets a custom TTL (Time-to-Live) value for packets sent during the scan. TTL determines how many network hops a packet can traverse before being dropped.

Can help evade detection if specific TTL values are expected by a firewall or IDS.  

**Caution:** Using incorrect TTL values might prevent packets from reaching the target.

```bash
nmap --ttl 64 <target>
```

#### --data-length

This flag appends a specified amount of random data to the packets sent during the scan. This helps to evade detection by firewalls or IDS systems that inspect packet sizes and signatures.

By adding extra data, the scan traffic becomes less predictable, potentially bypassing simple signature-based defenses.

```bash
nmap --data-length 50 <target>
```

#### -D (Decoy)

The `-D` flag enables decoy scanning, where Nmap sends scan packets from multiple spoofed IP addresses along with your real IP, making it harder for the target to identify the true source of the scan. This helps to obscure the origin of the scan by mixing it with traffic from decoy addresses.

This technic is useful for bypassing logging or attribution attempts.

```bash
nmap -D 192.168.1.2,192.168.1.3,ME <target>
```
- The keyword `ME` represents your real IP.