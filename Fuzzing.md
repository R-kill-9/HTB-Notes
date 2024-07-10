**Fuzzing** is an automated software testing method that injects invalid, malformed, or unexpected inputs into a system to reveal software defects and vulnerabilities. A fuzzing tool injects these inputs into the system and then monitors for exceptions such as crashes or information leakage.
# Gobuster
It is a command-line tool used for performing brute-force scans or directory and subdomain enumeration on a website.
- To find subdirectories:
````bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#wordlist example: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
#machine example: 10.10.192.23 or http://10.10.192.23:80
#-q to don't print the errors
gobuster dir -u <machine-ip> -w <wordlist> -o gobuster.out -t 200
````

- To find subdomains:
```bash
#wordlist example: /usr/share/dnsrecon/subdomains-top1mil-20000.txt
#machine ip example: 10.10.192.25
gobuster vhost -w <wordlist> -u <machine-ip> -o gobuster.out
````

# wfuzz
It is a command-line tool used for performing brute-force scans or directory and subdomain enumeration on a website. Also, it can be useful for enumerate files with an specific extension.
- To find subdomains:
```bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#machine example: 10.10.192.23
#-c print with colours
#--hc <status> don't print outuput with this status. For example: --hc 404
wfuzz -c  -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-20000.txt  -u http://<machine-ip> -H "Host: FUZZ.<machine-ip>" -t 10
```


- To find subdirectories:
```bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#machine example: 10.10.192.23
#-c print with colours
#--hc 404 don't print errors
wfuzz -c --hc 404 -w <wordlist> http://<machine-ip>/FUZZ
```

- To find common files:
```bash
#wordlist example:/usr/share/wordlists/dirb/big.txt
#machine example: 10.10.192.23
#-c print with colours
#--hc 404 don't print errors
wfuzz -c --hc 404 -w <wordlist> http://<machine-ip>/FUZZ.php
```