Pivoting  is the process of using a compromised system as a gateway to access other machines or networks that are not directly reachable.

1. **Compromise a Host**
- Gain access to a machine using exploits in Metasploit, resulting in a **Meterpreter session** or other payload connection. 
- Identify a network that was not accessible before.

2. **Background the Meterpreter Session**

- Once you have a session, you need to background it to return to the main Metasploit console.

```bash
meterpreter > background
```

3. **Set Up Routes**

- Use the `autoroute` module to add a route through the compromised host. This will enable Metasploit to send traffic through the host to the target network.

```bash
run autoroute -s [subnet]
```

4. **Verify the Routes**

- Check the routes added to ensure connectivity:

```bash
msf6 > route
```

5. **Run Scans Through the Pivot**

- Perform reconnaissance using modules like `auxiliary/scanner/portscan/tcp` or `auxiliary/scanner/http/http_version` through the pivoted route.

```bash
use auxiliary/scanner/portscan/tcp
set RHOSTS <discovered_ip>
run
```