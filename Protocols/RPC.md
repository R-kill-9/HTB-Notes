The **Remote Procedure Call (RPC)** protocol enables software to execute code on a remote system as if it were local. In a Windows environment, RPC is integral to communication between services and client machines, often used for managing resources, retrieving system information, and interacting with Active Directory.

## Rpcclient
`rpcclient` is a tool in the Samba suite used to interact with Windows machines and enumerate information about SMB shares, user accounts, groups, and other domain-related data. 

#### Connecting to a Target

| Option          | Description                                                                                             |
|-----------------|---------------------------------------------------------------------------------------------------------|
| `-U <username>` | Specifies the username to authenticate with.                                                            |
| `<target_ip>`   | The IP address of the target machine.                                                                   |
| `-N`            | Attempts an anonymous login to the target machine.                                                      |

```bash
rpcclient -U <username> <target_ip>
```