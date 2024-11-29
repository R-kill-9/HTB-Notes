**Google Dorks** are advanced search queries or operators used to find specific information on websites by leveraging Google’s search engine. These queries help uncover sensitive data such as exposed files, login pages, database dumps, or misconfigured servers that are publicly accessible but not easily visible.

## site
The **`site:`** operator is used to restrict search results to a specific website or domain. It helps in finding information within a particular site without navigating through its pages manually.

```bash
site:<domain>
```
##### Subdomain enumeration
To perform subdomain enumeration, the wildcard character (`*`) can be used before the domain to indicate that we want to find all existing subdomains.

```bash
site:*.<domain>
```

## inurl
The **`inurl:`** operator is used to search for URLs containing a specific word or phrase. It helps in narrowing down results to pages with certain keywords in their web address.

```bash
site:<domain> inurl:<keyword>
```

- **`inurl:admin`** – Finds URLs with "admin" in the address (e.g., admin panels or dashboards).
- **`inurl:login`** – Searches for login pages.
- **`inurl:passwd.txt`** – Searches for password pages.

## intitle
The `intitle:` operator  searches for pages where the specified keyword appears in the title of the webpage. It's useful for narrowing down results to pages that are likely to focus on a specific topic or content.

```bash
site:<domain> intitle:<keyword>
```

##### Directory listing
When directory listing is enabled, sensitive information may be unintentionally exposed.

```bash
site:<domain> intitle:index of
```

## filetype
The `filetype:` operator is used to search for specific types of files on the web. It restricts results to files of a particular extension, such as PDFs, Word documents, or configuration files, making it useful for finding publicly accessible resources.

```bash
site:<domain> filetype:<extension> <keyword>
```