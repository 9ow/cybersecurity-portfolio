# Footprinting and OSINT field guide

Source: Unit 2 slides 4–27. Classroom tools and examples; no personal result verified.

Footprinting discovers public domain names, DNS records, possible subdomains, web technology, services, documents and organizational structure. Passive collection uses public indexes and third-party data; active collection contacts a scoped system and may leave logs. Public information is not permission to access private files.

Search operators: `site:example.com` restricts a domain; `filetype:pdf` finds indexed file types; `intitle:` / `allintitle:` match titles; `inurl:` / `allinurl:` URLs; `intext:` / `allintext:` body text; `OR` alternatives. Results can be stale, misleading or incomplete.

`ping <LAB_HOST>` tests ICMP reachability and RTT; failure does not prove host is down. IP TTL is a hop limit, not a guaranteed OS fingerprint. `traceroute <LAB_HOST>` / Windows `tracert` estimates hops and probe timing; missing hops may reflect filtering or asymmetry. `whois example.com` shows registry/name-server details when public, subject to privacy masking.

`nslookup -type=A example.com` finds IPv4 records; `AAAA` is IPv6; `CNAME` alias; `MX` mail exchange; `NS` name servers; `SOA` zone authority; `SRV` service records; `PTR` reverse DNS. Resolver caches, split-horizon views, and DNS changes limit certainty.

The slides introduce IP geolocation (approximate), HTTrack (active website copying—scope and bandwidth controls required), Netcraft (hosting/certificate history), theHarvester (public-source emails/domains), WhatWeb (technology heuristics), WAFW00F (WAF heuristics) and the Social Engineering Toolkit (human testing requires explicit permission). Treat tool output as leads, not independently verified vulnerabilities. Defenses include limited public disclosure, metadata hygiene, avoiding directory listing, security awareness and firewall/IDS monitoring.