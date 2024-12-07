**Email harvesting** is the process of collecting email addresses from various online sources, often for marketing or malicious purposes. It involves extracting email addresses from websites, forums, social media, or public directories using manual methods or automated tools like web scrapers.

## Harvester

[theHarvester](https://github.com/laramies/theHarvester) is a simple to use, yet powerful tool designed to be used during the reconnaissance stage of a red team assessment or penetration test. It performs open source intelligence (OSINT) gathering to help determine  a domain's external threat landscape. The tool gathers names, emails, IPs, subdomains, and URLs by using  
multiple public resources.

| Option | Description |
|--------|-------------|
| **`-d <domain>`** | Specifies the target domain to search (e.g., `example.com`). |
| **`-b <source>`** | Defines the source to query (e.g., Google, Bing, LinkedIn, etc.). Use `-b all` to query all available sources. |
| **`-l <limit>`** | Sets the maximum number of results to retrieve (optional). |
| **`-f <filename>`** | Exports results to a file (e.g., PDF or HTML). |

```bash
theHarvester -d <domain> -b <source>
```

