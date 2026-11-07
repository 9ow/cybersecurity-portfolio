# Architecture, IPv4 Addressing and VLANs

## Goal
Build a four-site enterprise in Cisco Packet Tracer with **Bahrain as the central WAN hub** and KSA, Oman and Qatar as branch sites. The simulated sites have routers, distribution and access switches, PCs, servers and wireless equipment.

| Site | Main private IPv4 range | Design routing protocol |
| --- | --- | --- |
| Bahrain | `10.10.0.0/16` | OSPF |
| KSA | `172.16.0.0/16` | EIGRP AS 10 |
| Oman | `192.168.0.0/16` | EIGRP AS 20 |
| Qatar | `172.20.0.0/16` | RIPv2 |

The submitted report also shows static routing and WAN backup; the above is the site routing **design**, not proof all dynamic protocols converged.

## VLAN segmentation — Bahrain example
The project uses VLAN 10 Customer Operations, 20 Management, 30 Administration, 40 Finance, 50 IT, 60 HR, 70 Risk and Compliance, 80 Marketing, 90 Servers and 100 Wi-Fi. The corresponding private subnets follow `10.10.X.0/24`, for example `10.10.50.0/24` for the IT VLAN and `10.10.90.0/24` for Servers. VLAN **999** is configured as the native/unused VLAN.

**Access ports** belong to a particular VLAN; **802.1Q trunks** carry multiple tagged VLANs between switches; the native VLAN normally travels untagged. The report's trunk output shows active trunking with VLAN 999 native and allowed VLANs 10–100,999.

Layer 3 switches create **SVIs** to route between VLANs. HSRP allows virtual gateways such as `10.10.10.1`. Security ACLs then restrict which departments can reach other networks.

## Evidence and lessons
- `show vlan brief`: created VLANs and port associations.
- `show interfaces trunk`: allowed/native VLANs and link mode.
- `show ip interface brief`: SVI addressing and operational status.

Creating a VLAN does not automatically prove correct access policy or application connectivity. Source report: pages 5–8 and 26–28.