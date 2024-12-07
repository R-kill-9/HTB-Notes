
# Chisel 
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

- **Local Port Forwarding**

Target machine:
```bash
./chisel server -p <port>
```
Local machine
```bash
chisel client <chisel server address>:<chisel server port> <local port to open>:<address to point to>:<port to point to on the target address>
```
- **Remote Port Forwarding** 

Local machine
```bash
chisel server -p 9999 --reverse
```
Target machine
```bash
./chisel client <local_ip>:<local_listener_port> R:<remote_port_to_open>:127.0.0.1:<target_machine_port_to_open>
```

- **Dynamic Port Forwarding**
```bash
./chisel client <server_ip>:<port> dynamic :<local_port>
```


# Netstat
**Netstat** (Network Statistics) is a command-line tool to display network connections, routing tables, and interface statistics. It can be useful to find open ports to execute a port forwarding.

#### **Key Flags**

| Option | Description |
|--------|-------------|
| **`-a`** | Show all connections and listening ports. |
| **`-n`** | Show numerical addresses and port numbers (no DNS resolution). |
| **`-t`** | Display TCP connections. |
| **`-u`** | Display UDP connections. |
| **`-l`** | Show only listening ports. |
| **`-p`** | Show the PID/program name associated with each connection. |


### **Basic Commands**

- **Show active connections**:
```bash
netstat -an
```
- **List listening ports**:
```bash
netstat -tuln
```




