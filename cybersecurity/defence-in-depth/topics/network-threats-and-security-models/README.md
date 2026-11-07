# Network Threats, Risk and Security Architecture

**Evidence:** lecture-derived conceptual learning. No executed attack simulation or personally observed telemetry is documented.

## Threat modelling vocabulary and risk decisions

A **threat** is a potential cause of harm; a **vulnerability** is the exploitable weakness (unpatched software, exposed management port or misleading trust boundary); **risk** concerns the likelihood and impact of exploitation; **mitigation** reduces either likelihood or impact. A *threat actor* is not the same as an attack vector. The lecture distinguishes external actors arriving over untrusted links and internal risks from users, compromised hosts or misconfiguration. Security policy translates risk decisions into enforceable operating rules. Risk management separates **analysis** (assets, threats, weaknesses, likelihood/impact) from **response** (mitigate, accept, transfer or avoid). Acceptance is a conscious risk decision rather than an implemented technical safeguard.

**Attacker profiles:** script kiddies use ready-made tools; vulnerability brokers commercialise vulnerability information; cybercriminals tend to seek financial gain; hacktivists pursue social/political causes; state-sponsored operators may have strategic objectives. White-, grey- and black-hat terminology concerns authorization and intent and does not replace a formal scope-of-work.

**Reconnaissance** locates assets before exploitation: a ping sweep identifies responding hosts; a port scan tests exposed services. **Access attacks** target credentials, sessions or software weaknesses. **DoS** targets availability; **DDoS** coordinates many compromised devices (a botnet of zombies under operator/handler control). A TCP **SYN flood** consumes half-open connection handling, whereas an ICMP **Smurf** pattern amplifies replies through broadcast behaviour on vulnerable networks. An attacker can eavesdrop on unprotected traffic, use a sniffer to capture packets, spoof IP or MAC source identity, intercept or modify communication through a man-in-the-middle position, or misuse an exposed cryptographic key. Packet sniffing itself is a tool capability; authorization and purpose distinguish legitimate analysis from attack.

## Malware and human-focused intrusion

A **virus** typically depends on a host file or execution path; a **worm** self-propagates; a **Trojan** disguises malicious functionality as a trusted file; **ransomware** restricts access to data, often through encryption; **spyware** collects information covertly; **adware** shows unwanted advertising; **scareware** manipulates victims using alarming false claims; a **rootkit** conceals malicious activity or access. Stuxnet is presented in the study material as a worm affecting industrial control environments; that classification should not be confused with the political motive or impact of the campaign.

**Social engineering:** phishing impersonates a trusted sender; spear phishing targets a particular recipient; pretexting invents a credible scenario; tailgating exploits physical trust; quid pro quo offers a benefit for information or access; spam is a distribution channel, not always a phishing attempt. Defensive design includes verification through a separate channel, awareness training, physical controls and reporting. **Data-loss vectors** in the lecture include email/webmail, unencrypted devices, cloud storage, removable media, paper records and inadequate access rules. DLP is an exfiltration-control capability, not a replacement for classification or permissions.

The lecture surveys dual-use security tools: password auditing, packet crafting, scanners, sniffers, debugging/forensics, fuzzing and exploit testing. Fuzzers submit malformed or unexpected input to discover crashes or unexpected execution; coverage-guided, mutation-based and protocol-aware variants were mentioned. Their use is restricted to authorized scope.

## CIA and supporting controls

| Property | Failure mode | Primary defensive ideas |
| --- | --- | --- |
| **Confidentiality** | Data copied or read without authority | Encryption, access control, controlled disclosure |
| **Integrity** | Data altered or replaced | Hashes/HMAC, signatures, change control, audit trails |
| **Availability** | Service becomes unreachable | Redundancy, capacity, hardening, tested backups and DoS resilience |

Encryption does not by itself prove integrity; a plain unkeyed hash does not authenticate who sent a message. Backups contribute to recovery only if restoration works. A copied confidential database is a confidentiality incident even when availability is unaffected.

Security domains also include asset inventory, human resources, physical/environmental safeguards, secure development and operations, incident response, business continuity and compliance. Network controls depend on organisational policy and people.

## Network Foundation Protection: three functional planes

Imagine a router with routing peers at the top, administrators entering through a management channel and user packets crossing through interfaces:

1. **Control plane — decide:** OSPF/EIGRP exchanges and routing calculations determine paths. Routing peer authentication and **CoPP** limit unwanted traffic to router CPU functions; CoPP classifies traffic then applies policing, not ordinary transit filtering.
2. **Management plane — administer:** Console, SSH/HTTPS, SNMP and logging permit controlled changes and monitoring. Restrict management sources, enforce identity and roles, record access and use secure transport instead of Telnet.
3. **Data plane — forward:** Forwarding tables direct packets; interface ACLs, antispoofing, port security, DHCP snooping and Dynamic ARP Inspection enforce traffic controls.

A diagram of the three planes would show routing protocols feeding the forwarding table, packet flows using that table and a distinct administrator connection changing/observing device state. An ACL protecting forwarded packets cannot replace login authorization; router login security cannot prevent a rogue DHCP server.

## Perimeter, defence in depth and Zero Trust

A traditional perimeter assumes internal networks are more trusted than outside networks. This is brittle when laptops, BYOD, cloud services and compromised inside hosts cross boundaries. **Defence in depth** combines independent barriers—identity, segmentation, host controls, firewalling, monitoring, backups and response—so one failure does not expose everything. **Zero Trust** removes implicit access based on location: policy assesses user, device condition, resource sensitivity and context for each access decision, then limits scope and movement. A conceptual decision path is: user/device request → identity and device-condition checks → policy decision → narrowly scoped access → continuing monitoring. Zero Trust is not “deny all access”; it requires conditional authorization. Legacy integration, operational complexity and continuous monitoring are real design constraints.

**What I learned:** attack category and threatened CIA property determine the appropriate control, and protection must cover all three network planes rather than only the Internet edge. **Verification boundary:** threat examples and diagrams are theoretical; no authorized packet captures, scan results or attack logs were supplied. See [practical exercise register](../../PRACTICAL_EVIDENCE.md).
