# Network Configuration Verification — What I Tested and Learned

The original 48-page Packet Tracer report includes configuration outputs and sampled connectivity tests. Each command proves a particular state, not necessarily complete end-to-end security.

| Verification | Purpose |
| --- | --- |
| `show vlan brief` | Verify VLANs and local access-port assignments |
| `show interfaces trunk` | Check trunk state, allowed VLANs and native VLAN |
| `show ip interface brief` | Check IPv4 addresses and interface up/down state |
| `show ip route` | Inspect selected routes and backup next-hop configuration |
| `show spanning-tree summary` | Observe root/forwarding/blocked Layer 2 paths |
| `show standby brief` | Check HSRP active/standby state and virtual IP |
| `show port-security` | Inspect MAC limits, security state and violations |
| `show ip dhcp snooping` | Verify feature enabled status, trusted uplinks and VLANs |
| `show access-lists` | Inspect ordered permit/deny rules and counters |
| `show ip nat translations` | Observe mapped services or active translations |

## Actual observations in the report
- IT SSH login succeeds, whereas a non-IT management connection is closed.
- Server ICMP tests fail, while an HTTP browser screenshot demonstrates the selected web application is reachable under a different policy.
- Same-department remote ping succeeds; unrelated department traffic is blocked in selected tests.
- STP reports blocked and forwarding paths; HSRP reports active and standby gateway roles.
- DHCP snooping is disabled in one earlier screenshot and enabled in later implementation output.
- One port-security screenshot shows secure-down; don't infer active forwarding from merely having an address limit configured.
- NAT tables and configurations show server service mappings. End-to-end Internet reachability needs testing in addition to matching configuration.

## Troubleshooting approach
Start with interface status, VLAN and trunk. Then validate SVI/HSRP gateway, routing table, ACL placement and NAT where appropriate. For each screenshot record the action, expected result, actual result and what uncertainty remains.

**Image publication:** the screenshots exist in the *original report*, but original binaries are not yet on GitHub. They require a privacy review for personal identifiers, passphrases and secrets. Reference report pages 5–47.