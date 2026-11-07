# Network Address Translation

**Source:** `Firewall NAT Technologies.pptx`. Topic/week placement provisional. **Not recorded as studied or practical exercise-completed.**

## NAT essentials
- NAT addresses IPv4 scarcity; source private ranges: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`. Public directly Internet usable, private not.
- NAT policy: post-translation address (pool or outbound interface) + source/destination address, zones, egress interface, service, time + action.
- NAT policies processed top-down on first match. **Bidirectional/destination** NAT groups precede **source** NAT and can't be reordered behind source.
- Source NAT: internal client → external; destination NAT: public → internal server; bidirectional: translates source and destination. Advantages: reuse and privacy; disadvantages: complicates monitoring/restricts applications.

## Source NAT mode comparison
| Mode | Translation | Distinguishing behavior |
|---|---|---|
| **No-PAT** | 1:1 IP only, no ports | Same ports; needs enough public addresses |
| **NAPT** | IP + source port | Many private clients share few public IPs |
| **Easy IP** | IP + port | Uses **WAN interface address** instead of pool; PPPoE example |
| **Triplet NAT** | IP + port, creates server mappings | External peers can initiate audio/video/file-sharing flows |

## Source NAT configuration shown in PPT
```text
[FW] nat address-group group1
[FW-address-group-addressgroup1] mode pat
[FW-address-group-addressgroup1] section 0 1.1.1.10 1.1.1.15
[FW-address-group-addressgroup1] route enable
[FW] nat-policy
[FW-policy-nat] rule name policy1
[FW-policy-nat-rule-policy1] source-zone trust
[FW-policy-nat-rule-policy1] destination-zone untrust
[FW-policy-nat-rule-policy1] source-address 10.1.1.0 24
[FW-policy-nat-rule-policy1] action source-nat address-group group1
```
PPT also requires corresponding `security-policy`, firewall interfaces/zones and default route.

## Destination, bidirectional and ALG
- Destination NAT translates public destination to private; **static** fixed mapping, **dynamic** no fixed mapping. Example address group `10.2.0.7 10.2.0.8` with `action destination-nat static address-to-address address-group group1`.
- Bidirectional NAT translates both source and destination in same flow; can remove need to configure gateway on intranet server in the diagram's case.
- **ASPF** application-aware packet filtering / expected data mapping vs **NAT ALG** rewriting IP/port embedded in application payload.
- **NAT Server** statically maps public IP/port to an internal server; PPT example `nat server policy_ftp protocol tcp global 1.1.1.10 ftp inside 10.2.0.8 ftp unr-route` then `detect ftp`. Route example: `ip route-static 0.0.0.0 0.0.0.0 1.1.1.254`.

No practical exercise worksheet or executed configuration is established.
