**Chisel** is a TCP/UDP tunnel over HTTP that enables secure port forwarding, often used in penetration testing to bypass firewalls and NAT.

- You can download the Chisel last releases here: [link](https://github.com/jpillora/chisel/releases)
- Good explanation of how to use it: [explanation](https://deephacking.tech/pivoting-con-chisel/)
### Usage
First, you need to start **chisel** at server mode server on the machine you want to access.
```bash
./chisel server -p <port>
```
If you want to access using the remote mode you will need to use:
```bash
./chisel server -p 9999 --reverse
```

**Local Port Forwarding**

Allows forwarding traffic from a local port to a specific port on the target machine through the Chisel server.

*Target machine*
```bash
./chisel server -p <port>
```
*Local machine*
```bash
chisel client <chisel server address>:<chisel server port> <local port to open>:<address to point to>:<port to point to on the target address>
```

**Remote Port Forwarding** 

Allows opening a port on the **target machine** (via the Chisel client) that points to a service on the **local machine**.

*Local machine*
```bash
chisel server -p 9999 --reverse
```
*Target machine*
```bash
./chisel client <local_ip>:<local_listener_port> R:<remote_port_to_open>:127.0.0.1:<target_machine_port_to_open>
```

**Dynamic Port Forwarding**

Creates a local SOCKS proxy that dynamically forwards traffic to any destination through the Chisel server.

```bash
./chisel client <server_ip>:<port> dynamic :<local_port>
```

