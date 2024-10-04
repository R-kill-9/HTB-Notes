**LDAP** is a protocol for accessing and managing directory information used to search and modify information in a directory.It allows for the management of information about users, groups, permissions, and other objects within a network. Commonly used in enterprise applications, especially with Microsoft Active Directory.

## ldapsearch
- **Anonymous Search**: Attempt to retrieve information without credentials:
```bash
ldapsearch -x -H ldap://<server_ip> -b "dc=example,dc=com"
```

- Find users with specific attributes (like emails):
```bash
ldapsearch -x -H ldap://<server_ip> -b "dc=example,dc=com" "(objectClass=person)" mail
```
## Nmap
- Discover open LDAP ports and services:
```bash
nmap -p 389,636 <target_ip>
```

- Script scanning for LDAP:
```bash
nmap -p 389 --script ldap* <target_ip>
```

## LDAPenum
To enumerate all users in an LDAP directory:

```bash
ldapenum -u <username> -p <password> -H ldap://<server_ip>
```

## Hydra
Perform brute-force attacks on LDAP authentication:
```bash
hydra -L <username_list> -P <password_list> ldap://<target_ip>
```