# STP, HSRP and Redundant WAN Paths

## Three kinds of redundancy
**STP/PVST** prevents Ethernet loops in a topology with redundant physical switch links. The report shows some ports in forwarding and others in alternate/blocking states. A blocked backup path can be the correct healthy state.

**HSRP** provides a virtual default gateway across two Layer 3 switches. The `show standby brief` screenshots show active and standby roles across VLAN groups, example priorities **110** and **90**. HSRP protects a first-hop gateway, not a remote WAN link.

**Dual WAN links:** each branch is designed with a primary and backup serial path to Bahrain. A floating static backup route has a larger administrative distance than the preferred route, allowing failover when the primary route is removed under appropriate conditions.

## Oman WAN example
| Path | Bahrain IP | Oman IP | PPP authentication |
| --- | --- | --- | --- |
| Primary | `10.255.2.1` | `10.255.2.2` | CHAP |
| Backup | `10.255.22.1` | `10.255.22.2` | PAP |

**CHAP** is challenge-response authentication; **PAP** is weaker because of its password-handling design. The report's PAP use reflects the exercise, not a modern production security recommendation.

## Verification
`show spanning-tree summary` and interface state reveal chosen Layer 2 paths. `show standby brief` shows active/standby gateways. `show ip interface brief` and `show ip route` show link addresses and selected routes.

The report demonstrates configured redundancy; full service continuity after simulated failure should be tested explicitly. Sources: pages 11–16 and 34–40.