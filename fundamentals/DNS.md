# DNS and DNSSEC

## DNS
DNS consists of a distributed database of domain names and IP addresses, linked together in a hierarchy. It is used to translate human-readable domain names into IP addresses.

### DNS Record Types
- **A Record**: Maps a domain name to an IP address.
- **CNAME Record**: Maps a domain name to another domain name.
- **MX Record**: Maps a domain name to a list of mail exchange servers.
- **NS Record**: Maps a domain name to a list of DNS servers authoritative for the domain.
- **PTR Record**: Maps an IP address to a domain name.
- **SOA Record**: Specifies the DNS server providing authoritative information about a domain.
- **TXT Record**: Holds text information.

### DNS Resolution
1. **Local DNS Resolver**: The client queries the local DNS resolver.
2. **Root DNS Servers**: The local DNS resolver queries the root DNS servers.
3. **TLD DNS Servers**: The root DNS servers return the TLD DNS servers for the domain.
4. **Authoritative DNS Servers**: The TLD DNS servers return the authoritative DNS servers for the domain.

### Domain registration
To register a domain, you need to provide the domain registrar with the domain name, contact information, and the DNS servers that will be authoritative for the domain.
1. register the domain with a domain registrar.
2. provide the domain registrar with the DNS servers that will be authoritative for the domain.
3. The domain registrar updates the root DNS servers with the authoritative DNS servers for the domain.
4. The root DNS servers return the authoritative DNS servers for the domain (TLD DNS servers).

### DNS Cache
DNS resolvers cache DNS records to reduce latency and the load on authoritative DNS servers. The Time-To-Live (TTL) value in the DNS record determines how long the record can be cached.

### DNSSEC
DNSSEC is a set of extensions to DNS that provides authentication and integrity to DNS responses. It uses digital signatures to verify the authenticity of DNS data.

DNSSEC is an extra layer on top of DNS that provides a way to check if the DNS data is valid. It uses public key cryptography to sign DNS records and verify their authenticity.
