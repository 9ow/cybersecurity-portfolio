# Ethical Hacking | Technical Security Portfolio

A structured knowledge base on authorized offensive security assessment, developed around information security fundamentals, reconnaissance, network scanning, service enumeration, vulnerability management, adversary frameworks and technical reporting.

**Focus:** explain real protocol behavior, command semantics, what results do and do not prove, operational limitations, and practical defensive implications. Commands use synthetic targets. The repository does not imply ownership of any tested environment or independently verified exploitation.

## Technical index

| Area | In-depth documentation |
|---|---|
| Security principles, assessment scope and ethics | [Security principles and engagements](topics/ethical-hacking-foundations/security-principles-and-engagements.md) |
| Reconnaissance, OSINT, DNS and fingerprinting | [OSINT techniques and tooling](topics/reconnaissance-and-osint/osint-techniques-and-tooling.md) |
| Network discovery, TCP/UDP states, Nmap and output | [Nmap command reference](topics/network-scanning-and-enumeration/nmap-command-reference.md) |
| NSE categories, service checks and result validation | [NSE and service assessment](topics/network-scanning-and-enumeration/nse-and-service-assessment.md) |
| SNMP objects, OIDs, agents and management exposure | [SNMP enumeration](topics/network-scanning-and-enumeration/snmp-enumeration.md) |
| LDAP base DNs, filters, schema and query outcomes | [LDAP enumeration](topics/network-scanning-and-enumeration/ldap-enumeration.md) |
| SMTP, FTP, SMB and NetBIOS protocol behavior | [Service enumeration](topics/network-scanning-and-enumeration/smtp-ftp-and-netbios.md) |
| Vulnerability scoring, CVE, CWE and validation | [Scoring and validation](topics/vulnerability-assessment-reference/scoring-and-validation.md) |
| MITRE frameworks, attacker behavior and AI security | [Threat models and AI](topics/adversary-frameworks-reference/threat-models-and-ai.md) |
| Methodology, reproducibility and evidence quality | [Technical reporting and quality](topics/reporting-reference/technical-reporting-and-quality.md) |

[Browse the technical techniques index](techniques/README.md).

## Skills demonstrated through documentation

- Explain reconnaissance workflows, public-source limitations, common DNS record types and domain intelligence.
- Interpret packet-level port scan outcomes, scan uncertainty, TCP control flags and UDP filtering.
- Compare Nmap discovery, transport, version identification, timing, scripting and output options.
- Explain how SNMP and LDAP expose structured management or directory data, how queries are composed, and which controls reduce disclosure.
- Analyze SMTP response codes, FTP authentication signals and network sharing exposure without overclaiming access.
- Distinguish CVE identifiers, CWE weakness taxonomies, CVSS vectors, scanner flags and actual risk.
- Translate technical observations into defensible, appropriately qualified findings and mitigation advice.
- Evaluate AI-assisted security workflows with human review, scope control and data minimization.

## Professional standards

This repository separates source-derived technical explanations and illustrative command syntax from individually verified execution. No real system addresses, private hostnames, credentials, organization-specific infrastructure or personal identity details are included. No third-party demonstration screenshots are presented as personal work. Testing is permissible only with written authorization and defined scope.

The material represents knowledge and disciplined technical reasoning; it is not represented as an independently conducted client assessment, credential or employment history.