# Reconnaissance And OSINT

## What footprinting means
Footprinting gathers information about a target's visible infrastructure and organization. The lecture identifies domains, IP addresses, network paths, technologies and exposed services as useful context. This can guide an authorized assessment but is not a confirmed vulnerability.

## Passive versus active collection
**Passive collection** uses already publicly accessible information with minimal direct interaction with target systems. **Active collection** sends traffic or otherwise contacts target-controlled resources and can appear in their logs. The difference matters for scope and authorization.

## Public information sources covered
The source slides explain search-engine operators such as domain restriction with `site:`, title terms with `intitle:`, URLs with `inurl:`, and text search with `intext:`. Domain registration records may reveal ownership clues, but public records may be missing or outdated. DNS lookups distinguish address records from authority metadata.

## Interpreting reachability and network paths
ICMP echo results provide a point-in-time reachability observation and may be filtered. Traceroute-style utilities show intermediate path clues, but missing hop replies do not necessarily show packet loss to the destination.

## Web technology identification
The lecture introduces website metadata and technology-fingerprinting tools, public email/domain enumeration, and web application firewall identification. Tool output needs validation: detecting a software family or apparent product does not automatically prove a weakness.

## Why social engineering is connected
Names, roles and exposed services can be assembled into more persuasive phishing attempts. Ethical investigators should limit unnecessary collection and avoid sharing personal details.

## Lab status
A synchronous footprinting lab was previously reported completed. Specific observed screenshots and command outputs were not available for independent confirmation; future uploads should explain tool, goal, permitted scope and output.