# wpscan
**WPScan** is a widely-used open-source security scanner specifically designed to detect vulnerabilities in WordPress websites.
- `--url `: Specifies the URL of the WordPress website you want to scan.
- `--enumerate`: Enumerates vulnerable plugins (`vp`), users (`u`), themes (`t`), and timthumbs (`p`).
- `--plugins-detection mixed`: Specifies the plugin detection mode. In this case, it's set to "mixed," which includes both passive and aggressive detection methods.
- `--passwords`: Specifies a file containing a list of passwords to use for brute force attacks.
- `--usernames`: Specifies a single username to use for brute force attacks.
- `--exclude-content-length`: Excludes the Content-Length header from requests.
- `--proxy`: Specifies a proxy to use for the scan.
- `--random-agent`: Uses a random User-Agent for each request.
- `--verbose`: Increases the verbosity level of the output, providing more detailed information about the scan process.
## Basic usage
```bash
wpscan --url <url>
```
## Other options
```bash
wpscan --enumerate vp,u,t,p \
       --plugins-detection mixed \
       --passwords /path/to/passwords.txt \
       --usernames admin \
       --exclude-content-length \
       --proxy http://proxy.example.com:8080 \
       --random-agent \
       --verbose
```

# nuclei
*Nuclei* is a vulnerability scanner that can be used to identify and exploit vulnerabilities in web applications and other services.
It can be used to identify a wide range of vulnerabilities, including:

- **Injection vulnerabilities:** These vulnerabilities allow an attacker to inject malicious code into a target application.
- **Cross-site scripting (XSS) vulnerabilities:** These vulnerabilities allow an attacker to inject malicious code into a web page that is then executed by a victim's browser.
- **SQL injection vulnerabilities:** These vulnerabilities allow an attacker to inject malicious SQL code into a web application, which can then be used to steal data or gain unauthorized access.
- **Authentication vulnerabilities:** These vulnerabilities allow an attacker to bypass authentication and gain unauthorized access to a system.
## Parameters
- target / -u: Allows indicating a URL on which the tests will be performed.

- list / -l: Allows indicating a list of targets in a text file, one URL per line in the file.

- automatic-scan / -as: Executes an automatic scan using Wappalyzer to detect the architecture of the target.

- templates / -t: List of templates or directories containing templates separated by commas.
```bash
# url example: http://192.1689.199.45/login.php
nuclei -u <url> 
# you can filter for the severity
nuclei -u <url> -severity high,critical -o output.txt
```


# joomscan
*joomscan* is a vulnerability scanning tool specifically designed to identify and assess the security of websites using the Joomla content management system. Joomla is a popular content management system (CMS) used for creating and managing dynamic websites.

joomScan is primarily used to search and detect potential vulnerabilities in Joomla-based websites, including security flaws, insecure configurations, or weaknesses in system implementation.

