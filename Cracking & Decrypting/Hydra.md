**Hydra** supports a wide range of protocols, including HTTP, FTP, SMTP, Telnet, SSH, and many others. It works by sending multiple login attempts to the target system using a wordlist or custom dictionary file that contains potential usernames and passwords. Hydra then systematically tries each combination until it finds a successful login or exhausts all possibilities.
```bash
# password list example: 10-million-password-list-top-1000000.txt
# IP example: 10.10.10.10
# service example: ssh
# if you want to use a list of users the flag is -L
hydra -l <username> -P <password_list_path> <service>://<IP_or_domain_name> 
```

## Using hydra in a web login page
It can be useful intercept the petition with burp for extract the different fields. 
- url_path_page = Can be seen next to POST in the intercepted petition. It makes reference to the location of the login page inside the server.
- error_message: You need to do a wrong petition to obtain this field.
```bash
# t = threads
hydra -t 64 -l <username> -P <password_file_path> <IP_or_domain_name> http-post-form "<url_path_page>:username=<username>&password=^PASS^:<error_message>"
```
