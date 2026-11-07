# Reconnaissance, footprinting and open-source intelligence

## Collection model

Footprinting builds a contextual understanding of domains, nameservers, public services, web stacks, organizational structure and published documents. **Passive** methods examine information already made available by third parties or search indexes. **Active** methods query systems that belong to the scoped entity. “Public” does not imply reliable, current, unrestricted or safe to retrieve. An ethical workflow is: set inquiry → collect from a permitted source → record the date/source → triangulate → mark uncertainty → restrict stored personal information.

## Search engine operators

| Operator | Example on fictional data | What it actually does |
|---|---|---|
| `site:` | `site:example.com` | Limits results to pages indexed under a domain; not a complete inventory |
| `filetype:` | `filetype:pdf policy` | Finds indexed formats, not guaranteed all uploaded PDFs |
| `intitle:` | `intitle:"sign in"` | Matches title terms |
| `allintitle:` | `allintitle:admin dashboard` | Requires multiple title terms |
| `inurl:` | `inurl:portal` | Finds term in indexed URL |
| `allinurl:` | `allinurl:login php` | Requires multiple URL terms |
| `intext:` | `intext:"security policy"` | Matches body content |
| `allintext:` | `allintext:contact infrastructure team` | Matches all provided content terms |
| `OR` | `reconnaissance OR footprinting` | Finds alternatives |

Operators are search-provider-specific and may change. An indexed snippet can be stale; finding a sign-in path is not evidence of a misconfiguration, and exposed-looking files must not be retrieved when outside scope.

## Connectivity, RTT, TTL, MTU and routes

`ping <AUTHORIZED_HOST>` is an ICMP echo test on common platforms. A response helps establish reachability and round-trip time (RTT). RTT is a delay measurement of a particular path and moment; it is not internet speed or application response time. TTL is an IP hop-limit field decremented by routers; it is not a precise operating-system classifier. Path MTU limits the packet size that can traverse a path without fragmentation; ICMP filtering can interfere with path-MTU discovery. A host can decline echo replies while offering a functioning TCP service.

`tracert <AUTHORIZED_HOST>` on Windows and `traceroute <AUTHORIZED_HOST>` on Linux show a sequence of responding routers and probe RTTs. Three timings often represent three distinct probes. `*` can be no TTL-exceeded response, ICMP filtering or rate limiting. Asymmetric return paths, NAT and load balancing limit route conclusions; a missing intermediate response does not mean that hop is absent.

## DNS and WHOIS

```bash
nslookup -type=A example.com
nslookup -type=AAAA example.com
nslookup -type=MX example.com
nslookup -type=NS example.com
nslookup -type=SOA example.com
nslookup -type=TXT example.com
nslookup -type=SRV _sip._tcp.example.com
whois example.com
```

A maps a name to IPv4; AAAA to IPv6; MX prioritizes receiving mail hosts; NS delegates authoritative nameservers; SOA describes zone authority/serial and timer settings; CNAME aliases a canonical name; PTR reverse-maps an IP using reverse DNS; SRV points to named services; TXT commonly contains policy and verification strings. DNS resolvers may cache answers and enterprises may use split-horizon DNS. WHOIS registration, renewal, registrar and name-server fields are often masked by privacy services; registration contact details should not be harvested as private identity evidence.

DNS zone transfer is a separate TCP/53 operation intended between approved DNS servers; it can expose an entire zone if misconfigured. Testing it requires permission, and a failed transfer is an expected secure configuration for unrelated clients.

## Additional collection tools

- **theHarvester:** retrieves candidate email addresses, names and subdomains from selectable public sources. Coverage and API access vary; results can be incorrect or stale.
- **WhatWeb:** fingerprints web technologies using HTTP behavior and signatures; returned framework/version labels are hypotheses.
- **WAFW00F:** uses response behavior to infer a web application firewall; reverse proxies and custom responses can cause misidentification.
- **Netcraft:** historical hosting, certificate and infrastructure indicators; history does not prove current deployment.
- **IP location services:** geo-IP estimates are frequently coarse, VPN/proxy hosting may distort the location, and a city result must not be treated as a physical device address.
- **HTTrack:** makes a local copy of permitted site content; can produce high traffic, retrieve material unexpectedly, or violate site restrictions. Only controlled and authorized use.
- **Social Engineering Toolkit:** demonstrates impersonation-related risks; human contact, credential collection and phishing simulations require specific written consent and guardrails.

## What matters in the final analysis

Connect evidence to defensive outcomes: remove sensitive document metadata, restrict directory listing, reduce unnecessary exposure, enforce accessible security awareness, protect DNS zone transfers and monitor probing. Never present a guessed person, system location or compromised account as established fact. A research lead must be labeled as such.