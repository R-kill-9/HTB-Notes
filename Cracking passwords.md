## hashid
The main purpose of **hashid** is to identify the hash algorithm used so that you can select the appropriate tool to work with it, such as a cracking tool or integrity verification tool.
```bash
hashid <hash>
```

## hydra
Hydra supports a wide range of protocols, including HTTP, FTP, SMTP, Telnet, SSH, and many others. It works by sending multiple login attempts to the target system using a wordlist or custom dictionary file that contains potential usernames and passwords. Hydra then systematically tries each combination until it finds a successful login or exhausts all possibilities.
```bash
hydra -l <username> -P <password_file_path> <IP_or_domain_name>
```
## hashcat
It's a password cracking tool used for recovering passwords from various hash types. Hashcat supports a wide range of hash algorithms, including common ones like MD5, SHA1, SHA256, as well as more advanced ones like bcrypt, scrypt, and Argon2. It can handle both single hashes and hash lists, making it useful for cracking passwords stored in databases, files, or captured network traffic.
#### Parameters:
- The `-a` parameter (attack mode) in Hashcat determines the type of attack to be performed. Here are some common options:

	- `-a 0`: Dictionary attack. Hashcat will try different words or word combinations from a predefined dictionary.
	- `-a 1`: Brute-force attack. Hashcat will try all possible combinations of characters until a match is found.
	- `-a 3`: Mask attack. Hashcat allows specifying a custom pattern or mask to generate possible word combinations.
	- Other modes are also available, such as custom rules (`-a 6`) or hybrid attacks (`-a 7`) that combine multiple approaches.

- The `-m` parameter (hash type) indicates the type of hash to be cracked. Hashcat supports a wide range of hash algorithms, and each has an associated identification number. For example:

	- `-m 0`: MD5
	- `-m 100`: SHA1
	- `-m 500`: HMAC-SHA256
	- `-m 1800`: sha512crypt

```bash
# wordlist example: /usr/share/wordlists/rockyou.txt
hashcat -a 0 -m 0 <hash_file> <wordlist>
```
## John the Ripper
**John the Ripper** is a free password cracking software tool. It is among the  most frequently used password testing and breaking programs as it combines a number of  password crackers into one package, autodetects password hash types, and includes a  
customizable cracker. It can be run against various encrypted password formats  including several crypt password hash types most commonly found on various Unix  versions (based on DES, MD5, or Blowfish), Kerberos AFS, and Windows NT/2000/XP/2003 LM  
hash.

### Converting to hash
We will need converting to hash our files to being able to use John the Ripper.
- ZIP 
```bash
zip2john <zip_file> > <hash_file_generated>
```


### Cracking password

```bash
# wordlist example: /usr/share/wordlists/rockyou.txt
john -wordlist=<wordlist> <hash_file>
```
Once we have already used the previous command, we can see the password and username found using:
```bash
john --show <hash_file>
```