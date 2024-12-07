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

| Option                                             | Description |
|----------------------------------------------------|-------------|
| **`-l <username>`**                                | Specify the username (e.g., admin). Use `-L <file>` for a username list. |
| **`-P <password_list>`**                           | Provide the path to the password list. |
| **`-f`**                                          | Stop after the first successful attempt. |
| **`<target_IP_or_URL>`**                           | Target IP address or domain name. |
| **`http-post-form`**                               | Specifies the HTTP method and login form details. |
| **`/path_to_login_form`**                          | The URI path of the login form (e.g., `/login.php`). |
| **`username_field=^USER^&password_field=^PASS^`**  | Replace `username_field` and `password_field` with the actual form parameter names. |
| **`error_message`**                                | The response text shown when login fails (e.g., "Invalid username or password"). |


```bash
# t = threads
hydra -t 64 -l <username> -P <password_list> -f <target_IP_or_URL> http-post-form "/path_to_login_form:username_field=^USER^&password_field=^PASS^:error_message"
```
