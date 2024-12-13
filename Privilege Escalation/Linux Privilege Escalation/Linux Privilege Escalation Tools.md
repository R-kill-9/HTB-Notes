## Escalation ideas 
https://github.com/RoqueNight/Linux-Privilege-Escalation-Basics

# gtfobins
GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems.
link -> https://gtfobins.github.io

# sudo -l
Command used to know what commands can be executed as root by the actual user.

# getcap
**getcap** is used to query the security capabilities of a file in Linux-based systems. These capabilities provide finer-grained control over file access permissions, allowing certain programs to have access only to specific capabilities they need, rather than granting them full access to a file.
```bash
getcap -r / 2>/dev/null
```
# find
This command is used to search for files and directories within a specified directory hierarchy. It searches recursively through the directory structure, starting from the given directory, and matches files and directories based on specified criteria.

- Parameters:
	 - `-name <pattern>`: Matches files and directories with the specified name pattern.
	- `-type <type>`: Matches files or directories of the specified type, such as `f` for regular files or `d` for directories.
	- `-size <size>`: Matches files based on size, such as `+10M` for files larger than 10 megabytes or `-100K` for files smaller than 100 kilobytes.
	- `-user <username>`: Matches files owned by the specified username.

```bash
find [path] [expression]
```

**find** can be useful to discover all the files that can be executed with root privileges because of their SUID bit is enabled.
```bash
find / -perm -4000 2>/dev/null
```
After executing the command can be useful check the binaries with **GTFOBINS**.

# linpeas.sh
It is a script designed to assist in privilege escalation enumeration on Linux systems.
Linpeas is written in Bash scripting language and is designed to be executed directly on the target Linux system. It automates the process of gathering information and performing various checks to identify potential privilege escalation vectors.
**It's important paying attention to all the fields, specially the capabilities**
```bash
./linpeas.sh
```

# pspy
**pspy** is based on the analysis of the `/proc` directory, which contains information about the running processes in the Linux operating system. It utilizes the virtual file system `/proc` to obtain real-time information about processes, such as the process ID, process name, user executing the process, files opened by the process, and other relevant details.
```bash
./pspy
```

# /etc/passwd
This is a file that we can find in all the Linux machines. Once we have gained access to a machine and we want to escalate our privileges we can take a look to this file to see what users are registered in the machine. The fields that we can find for each row are: 
 - Username
 - Password
 - User ID
 - Primary Group ID 
 - User Information
 - Home Directory
 - Shell
```bash
cat /etc/passwd

#Example of a row:
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
```

# /etc/hosts
This file can be a valuable resource for mapping domain names to IP addresses within a target system.
For example, we could find a new subdomain.
```bash
ls /etc/hosts
```

# /proc/version
The proc filesystem (procfs) provides information about the target system processes. You will find proc on many different Linux flavours, making it an essential tool to have in your arsenal.

Looking at `/proc/version` may give you information on the kernel version and additional data such as whether a compiler (e.g. GCC) is installed.
This can be useful if you want to find a possible CVE.

# /etc/crontab
Each user on the system have their crontab file and can run specific tasks whether they are logged in or not. As you can expect, our goal will be to find a cron job set by root and have it run our script, ideally a shell.

# id
Something we can do to gain privileges is to observe the groups our current user belongs to, to see if there's any uncommon one and take advantage of it to exploit a vulnerability.
```bash
#command:
id                                     
#possible oeutput:
uid=1000(robert) gid=1000(robert) groups=1000(robert),1001(bugtracker)
```
If we observe the output, we can see that Robert is in the bugtracker group, what it's not common.

# locate
It is a command that locates if there is any file with this name. This can be useful, for example, if we want to locate a user or a group.
```bash
#command:
locate bugtracker
#possible output:
/usr/bin/bugtracker
```

# Path Hijacking
Path hijacking occurs when an attacker manipulates the $PATH variable to force the system to execute a malicious file instead of the intended command. For doing that, the attacker places a directory under his control at the beginning of $PATH.
#### Example
- Look for a file that can be executed as root.
```bash
sudo -l
```
- Find where is this file located and if the location is included in the path.
```bash 
whereis <file>
echo $PATH
```
- Create a new file with the exploit code and locate it inside a known directory.
- Modify the $PATH to point to the chosen directory.
```bash
export PATH=/<directory>:$PATH
```
 

