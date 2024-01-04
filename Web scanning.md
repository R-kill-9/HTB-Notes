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

# Cookies
- It can be very useful checking the cookies of a web-site. For example if we are on a web and we have this parameters on the cookie's storage table:
	- role: guest
	- user: 24322
- We will know that we are identified by our role and  id, so we can try to change these fields to gain access to other users information.
	- role: admin
	- user: 34322

