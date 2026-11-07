# Firewall Security Policies

**Source:** `Firewall Security Policies(1).pptx` (31 technical materials). Five teaching blocks discussed. No verified practical exercise execution.

## technical materials 5–9 — zones
- Zone contains one or more firewall interfaces; checks triggered for inter-zone traffic. Configurable defaults: **Trust** internal users, **DMZ** internal servers, **Untrust** Internet.
- **Local** = firewall itself; self-generated/self-processed packets are Local traffic. No interface can be *manually added* to Local; lecture also says all service interfaces belong to Local. Management via Telnet/web/SNMP requires Local-to-peer-zone security policy.
- Priority values in PPT table: **Local 100, Trust 85, DMZ 50, Untrust 5**, range **1–100**. Higher priority = higher trust; custom zones supported.

## technical materials 11–16 — policies
- Rule = matching conditions (5-tuples, users, time ranges) + permit/deny action; flows have direction. **First match** wins; default action **deny**.
- Specific-to-general ordering: block `172.16.1.1/32`, `172.16.1.2/32`, `172.16.1.3/32` prior to allowing `172.16.1.0/24`, Trust→Untrust:
```text
[FW] security-policy
[FW-policy-security] rule name policy1
[FW-policy-security-rule-policy1] source-zone trust
[FW-policy-security-rule-policy1] destination-zone untrust
[FW-policy-security-rule-policy1] source-address 172.16.1.1 32
[FW-policy-security-rule-policy1] source-address 172.16.1.2 32
[FW-policy-security-rule-policy1] source-address 172.16.1.3 32
[FW-policy-security-rule-policy1] action deny
[FW] security-policy
[FW-policy-security] rule name policy2
[FW-policy-security-rule-policy2] source-zone trust
[FW-policy-security-rule-policy2] destination-zone untrust
[FW-policy-security-rule-policy2] source-address 172.16.1.0 24
[FW-policy-security-rule-policy2] action permit
```

## technical materials 18–21 — stateful sessions
- Stateful inspection groups packets into related flows; new session follows successful first-packet inspection, later packets match session. The PPT includes TCP SYN/SYN+ACK/ACK diagram.
- Session tracks TCP/UDP/ICMP; **5-tuple** source/destination IP, source/destination port, protocol; **aging time** is time before deletion.
- `display firewall session table` standard; `display firewall session table verbose` with zone, TTL/Left, interface, next hop, MAC, packet and byte counts.

## technical materials 23–27 — ASPF
- **ASPF = Application Specific Packet Filter**; Telnet 23 and HTTP 80 are single-channel; FTP is multi-channel.
- Exam-critical: negotiations with dynamic addresses/ports → **server-map entry** (expected data channel) → first data packet generates **session**; no matching server map or session → normal security policy.
- Active FTP: client initiates control to TCP **21**, sends `PORT` with its negotiated IP/port; server initiates data from TCP **20**.
- Source commands: `firewall interzone trust dmz`, `detect ftp`, `display firewall server-map`, `display firewall session table`.

## technical materials 29–31 — applications
- Campus egress network border plus intranet protection: IP-based/user-based access control, tracing.
- Cloud: service isolation, reach VMs/portals using public addresses, resilience against single-device failure.
- Final T/F on session creation for ICMP Reply with stateful inspection disabled (discussed as True).

## Progress
Block 2 **2/3** (missed option unknown), Block 3 **3/3**, Block 4 **2/3** (missed option unknown); block 5 taught, full mock not recorded as completed. PPT examples ≠ commands executed in practical exercises.
