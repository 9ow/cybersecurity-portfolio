# SNMP: managed objects, queries and operational risk

**Simple Network Management Protocol** supports monitoring and management of network-capable agents. A manager queries an agent, usually via UDP/161; traps/informs commonly use UDP/162. An agent exposes objects described by MIBs (Management Information Bases), identified using hierarchical numeric OIDs (Object Identifiers). A returned value can be `STRING`, `INTEGER`, `Counter32`, `Gauge32`, `TimeTicks`, `IpAddress`, etc. These types matter when interpreting state and performance.

## Versions and authorization

SNMPv1/v2c commonly rely on read-only/read-write community strings. They provide weak confidentiality: strings and data are generally not encrypted. SNMPv3 supports user security models with authentication and optional privacy encryption, depending on configuration. Read-only is not necessarily safe to expose: banners, interface names, addresses, route tables, location, operating system and software identifiers help threat reconnaissance. Never publish community values even when trivial/default.

## Query examples and option anatomy

```bash
sudo nmap -sU -p 161 -Pn <AUTHORIZED_HOST>
snmpget -v2c -c <AUTHORIZED_COMMUNITY> <AUTHORIZED_HOST> .1.3.6.1.2.1.1.1.0
snmpwalk -v2c -c <AUTHORIZED_COMMUNITY> <AUTHORIZED_HOST> .1.3.6.1.2.1.2.2.1.2
snmpwalk -v2c -c <AUTHORIZED_COMMUNITY> <AUTHORIZED_HOST> .1.3.6.1.2.1.2.2.1.8
snmptranslate .1.3.6.1.2.1.1.1.0
```

`-v2c` selects SNMP v2c; `-c` supplies the community; the final numeric path is the requested object subtree. `snmpget` retrieves a single specific object (scalar OIDs commonly end in `.0`); `snmpwalk` traverses a subtree, often returning multiple indexed table rows. `snmptranslate` maps OIDs to names if appropriate MIB definitions are installed. The materials show configuring local MIB lookup via the system SNMP configuration and optional MIB packages.

## Important OIDs and how to interpret them

| OID / subtree | Meaning | Interpretation and caution |
|---|---|---|
| `.1.3.6.1.2.1.1.1.0` | `sysDescr.0` | Self-reported software/OS description; can be generic or stale |
| `.1.3.6.1.2.1.1.3.0` | `sysUpTime.0` | Time since management subsystem initialization, not necessarily total machine uptime |
| `.1.3.6.1.2.1.1.5.0` | `sysName.0` | Configured device name; may disclose internal naming conventions |
| `.1.3.6.1.2.1.2.2.1.2` | `ifDescr` | Indexed list of network interfaces (e.g., loopback and Ethernet) |
| `.1.3.6.1.2.1.2.2.1.8` | `ifOperStatus` | Values include 1=up, 2=down, 3=testing; not a guarantee that traffic can traverse |
| `.1.3.6.1.2.1.4.21` | Legacy `ipRouteTable` | Route destination/next-hop/metrics; implementation and IPv6 support vary |
| `.1.3.6.1.2.1.6` | TCP-related MIB | Connection metadata and counters; not all leaves represent listening ports |
| `.1.3.6.1.2.1.7` | UDP-related MIB | UDP counters and endpoint information, dependent on MIB implementation |
| `.1.3.6.1.4.1` | Enterprise vendor OIDs | Vendor-specific metrics; do not assume each value is universal |

The course material includes vendor UCD-SNMP `.2021.11.*` for CPU observations and `.2021.9.*` for disk resources. Percentage and counter units are distinct. An idle percentage near 94% signifies low recent measured utilization **for that metric and moment**, not that a server is permanently underutilized. Disk counters may use blocks rather than bytes. SNMP index suffixes identify a row or interface; never treat an index number as an IP address.

## Troubleshooting

- `open|filtered` on UDP/161: no definitive protocol response; use an authorized `snmpget` for confirmation.
- Timeout: check firewall/ACL, agent state, version, community/security user and UDP filtering. Do not brute-force community values.
- `No Such Object` or `No Such Instance`: MIB mismatch, missing instance index or access limitation; not proof that all SNMP is disabled.
- Numeric-only output: configure MIBs or use `snmptranslate`; preserve the numeric value in technical notes for accuracy.
- Unexpected interface status: correlate with management interface counters, time and endpoint configuration.

## Defensive controls

Disable unused SNMP, restrict queries to management networks, use SNMPv3 with authenticated encryption where supported, give the minimum MIB view required, remove default read/write access, log unexpected queries and review interface/route disclosures. Publicly presenting a fictionalized OID interpretation is appropriate; publishing actual inventory and routing information is not.