A **DNS zone transfer** is a mechanism used to replicate DNS records across different DNS servers. When a zone transfer is performed, a DNS server can send all of its DNS records to another DNS server, typically for backup or load balancing purposes. However, this can be risky, as it can expose sensitive DNS information about a domain if not properly secured.

## dig
To perform a zone transfer, you need to query a DNS server with the `AXFR` type. If the server is configured to allow zone transfers to external sources, you can retrieve all DNS records for the target domain.

```bash
dig @dns-server example.com AXFR
```