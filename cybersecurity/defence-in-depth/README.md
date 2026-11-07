# Defence in Depth | Network Security Engineering Portfolio

A technical learning portfolio on layered network defence, Cisco IOS security controls, access management, segmentation, inspection, endpoint protection and secure LAN operations. **This is a topic-organised engineering reference, not a weekly diary or a claim of production deployment.** It is based on the six uploaded lecture decks, study notes and quiz discussions. Worked examples are explicitly separated from independently verified hands-on results.

## Technical chapters

| Area | Engineering focus |
| --- | --- |
| [Threats, risk and security architecture](topics/network-threats-and-security-models/README.md) | Threat actors and vectors; malware; CIA; risk; NFP control, management and data planes; defence in depth and Zero Trust |
| [Device hardening and secure management](topics/network-device-hardening/README.md) | Console/VTY controls; SSH; authentication safeguards; privilege levels and CLI views; syslog; SNMPv3; NTP; routing authentication; resilient configuration |
| [Identity and AAA](topics/authentication-authorization-accounting/README.md) | Local vs server AAA; TACACS+ and RADIUS; authentication, authorization, accounting; method-list fallbacks; troubleshooting; 802.1X |
| [ACLs, firewall architecture and zone policies](topics/firewalls-acls-and-zone-policies/README.md) | ACL matching and order; wildcard masks; state tables; CBAC; DMZ; class maps, policy maps and directed zone pairs |
| [Intrusion detection and prevention](topics/intrusion-detection-and-prevention/README.md) | Passive IDS vs inline IPS; SPAN; atomic/composite signatures; detection engines; alarms, tuning and IOS IPS |
| [Endpoint and LAN controls](topics/integration-notes-pending/README.md) | Host defences; CAM overflow; port security; VLAN hopping; DHCP snooping; ARP inspection; combined control design |
| [Practical evidence register](PRACTICAL_EVIDENCE.md) | Separately scoped practical exercise worksheets, evidence gaps, verification criteria and privacy review |

## Evidence language

**Studied:** explicitly described in the supplied lecture technical materials and study discussions. **Illustrative configuration:** educational syntax reflecting those topics; it is *not* a claim that the commands ran on a device. **Verified hands-on:** requires original authorized practical exercise topology/configuration, device output and a specific expected-vs-observed test. There is currently **no independently verified hands-on result** in the supplied evidence. A syllabus activity, exercise question, worked answer or screenshot of a question is not execution evidence.

## Documentation conventions and boundaries

- Commands use placeholder addresses and identifiers from documentation ranges, or redacted values. No usable secrets or private network details are published.
- IOS command availability varies by platform, software train and licence. Validate against the actual practical exercise image before execution.
- A secure deployment must test authorized success, unauthorized denial, failover behaviour, logging and recovery; configuration text alone does not prove enforcement.
- Uploaded exam practice/dump documents were treated as **secondary prompts**, not authoritative configuration evidence. Their copyrighted question banks and answer keys have not been redistributed.
- No personal identities, student identifiers, grades, passwords, server secrets, private infrastructure, screenshots from a HomeLab, or unreviewed images are included.
- The existing folders and screenshot placeholders have been retained. The legacy [topic navigation](WEEKLY_INDEX.md) redirects here.

## Learning outcomes

I can explain how a control maps to a security objective and to a network plane; select source-based versus service-aware filtering; distinguish stateless rules from session-aware inspection; plan AAA and fallback without lockout; reason about ZPF directionality and default denial; understand sensor visibility and false alarms; and relate endpoint and Layer 2 controls to defence in depth. These outcomes represent **documented conceptual learning**, not verified device proficiency.
