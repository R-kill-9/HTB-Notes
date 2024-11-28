A **WAF** (Web Application Firewall) is a security system designed to monitor, filter, and block HTTP/HTTPS traffic to and from a web application. Its main purpose is to protect web applications from various attacks, such as SQL injection, cross-site scripting (XSS), and other OWASP Top 10 vulnerabilities.

## wafw00f
`WAFW00F` is an open-source tool used for detecting and identifying Web Application Firewalls (WAFs) that are protecting a web application.

```bash
wafw00f example.com
```

As we can see in the example, it shows that a WAF is protecting the application, in this case, Cloudflare.

![](Images/Wafw00f.png)