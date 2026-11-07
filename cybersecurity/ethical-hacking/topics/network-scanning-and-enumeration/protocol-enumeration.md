# Network protocol enumeration

Source: Unit 5 slides 3–45; commands illustrated here are lecture demonstrations or instructions, not verified personal work. All real endpoints and account names are replaced.

**Enumeration** interrogates responding services for machine names, shares, users, groups, routes, banners and settings. It is more active and detectable than passive research. Typical service endpoints include DNS TCP/53 for zone transfer, RPC TCP/135, NetBIOS UDP/137 and TCP/139, SMB TCP/445, SNMP UDP/161, LDAP 389, directory Global Catalog 3268, SMTP TCP/25. Listening does not imply permission to enumerate.

## NetBIOS and SMB

`nbtscan <LAB_HOST>` queries permitted NetBIOS names; enum4linux and SMB utilities can inspect allowed shares/accounts subject to authentication and OS policy. NetBIOS and direct SMB are distinct. Harden by disabling unnecessary NetBIOS, firewalling 137/139/445, enforcing share permissions and monitoring events.

## SNMP

SNMP managers read agent variables indexed by hierarchical **OIDs** and described by MIBs. SNMPv1/v2c community strings may be observable on the wire, whereas correctly configured SNMPv3 can offer authenticated encryption. `snmpget -v2c -c <LAB_COMMUNITY> <LAB_HOST> .1.3.6.1.2.1.1.1.0` reads `sysDescr.0`; `snmpwalk ... .1.3.6.1.2.1.2.2.1.2` lists interface descriptions; `.1.3.6.1.2.1.2.2.1.8` reports interface operational status (1 up, 2 down, 3 testing); `.1.3.6.1.2.1.4.21` accesses an older routing MIB. Unit 5 also shows `.1.3.6.1.2.1.6` (TCP), `.7` (UDP) and `.1.3.6.1.4.1` (vendor metrics). Interpret each leaf's type and MIB: counters are not automatically open ports. `snmptranslate` resolves numeric identifiers after local MIB installation. UDP `open|filtered` cannot confirm successful SNMP queries. Restrict management ACLs, enforce read-only least privilege, remove defaults and prefer SNMPv3.

## LDAP

LDAP provides directory entries with distinguished names (DN) and attributes. `ldapsearch -x -H ldap://<LAB_HOST> -s base namingContexts` queries the root DSE for naming context. After authorization to inspect a fictitious base, `ldapsearch -x -H ldap://<LAB_HOST> -b "dc=example,dc=test" "(objectClass=inetOrgPerson)" cn sn uid mail -LLL` lists matching user attributes; `(objectClass=posixGroup)` can show Unix group `gidNumber` and `memberUid`. `-x` uses simple bind rather than SASL, `-H` URI, `-b` base DN, `-s base` scope, `-LLL` concise LDIF. `result: 0 Success` is query success, not a security pass; empty results can mean access restriction. The lecture describes usernames/groups, **not** proof that plaintext passwords can be read. Mitigate anonymous information leakage, apply granular ACLs, use StartTLS/LDAPS and audit access.

## SMTP

SMTP TCP/25 transfers mail; 587 submission and 465 implicit-TLS submission are also discussed. In a permitted dummy SMTP service, connect using `telnet <LAB_HOST> 25` or `nc -nv <LAB_HOST> 25`, then `HELO lab.example`, `VRFY testuser`, `QUIT`. The slides introduce Metasploit `auxiliary/scanner/smtp/smtp_enum`, `smtp-user-enum`, and Nmap `smtp-enum-users` for approved account testing. Replies `250` and `252` can signal acceptance or inability to verify, but **252 is not proof of account existence**; `550 5.1.1` often means unknown. Catch-all policies, generic replies and rate limits make inference uncertain. Restrict VRFY/EXPN, use SMTP AUTH/TLS for submission and log attempted enumeration.

## FTP and other methods

FTP enumerates server banners, directories and access rights; `ftp-anon` tests anonymous access, while Unit 5 demonstrates Metasploit's `auxiliary/scanner/ftp/ftp_login` as a classroom example. Do not guess credentials, download data or alter files without separate permission. FTP may transmit credentials unencrypted; use protected transfer methods, disable unnecessary anonymous access, tighten directory permissions and log authentication. Slides also mention DNS, NTP, Telnet and AI-assisted analysis. A local Ollama summary of sanitized SNMP/LDAP output must be cross-checked against the original results and is not primary evidence.

**Evidence:** screenshots embedded in the lecture depict teacher demonstrations, not personally attributed executions; none were copied to the portfolio.