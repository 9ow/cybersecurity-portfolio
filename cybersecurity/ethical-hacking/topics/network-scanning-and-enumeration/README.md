# Network scanning and service enumeration

Network and application-level responses are interpreted in context rather than treated as automatic proof of a security flaw.

## Technical references

- [Nmap selection, host discovery, TCP/UDP probe mechanics, port states, timing and output](nmap-command-reference.md)
- [NSE scripting behavior, categories, named checks and verification](nse-and-service-assessment.md)
- [SNMP agents, community access, MIBs, OIDs, interfaces and routing data](snmp-enumeration.md)
- [LDAP directory schemas, search filters, base DNs and result interpretation](ldap-enumeration.md)
- [SMTP, FTP, SMB and NetBIOS exposure, protocol replies and controls](smtp-ftp-and-netbios.md)

**Technical principle:** a `filtered` or `open|filtered` result is uncertain; a returned product banner is not a proven CVE; a successful directory request is not necessarily unauthorized data disclosure. The guides provide targeted example syntax using synthetic systems.