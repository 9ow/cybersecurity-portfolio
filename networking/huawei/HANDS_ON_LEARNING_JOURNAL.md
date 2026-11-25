# Huawei Enterprise Network Security — Hands-on Learning Journal

**Platform:** Huawei eNSP / VRP / USG firewalls  
**Course context:** Enterprise Network Security and Firewall Technologies  
**Last updated:** 2026-11-25  
**Evidence level:** Learning journal compiled from guided practice and shared CLI output. Not a claim of production deployment or certification.

## Skills studied and practiced

| Area | What I learned | Evidence/status |
|---|---|---|
| VRP foundations | System/user views, interface configuration, saving and inspecting configuration, `display` diagnostics | Practiced during eNSP exercises; individual full configs not archived |
| IP addressing and connectivity | Configure firewall/router interfaces, /24 and /30 networks, default gateways, ping and link checks | In a VPN practice topology, PC1 successfully reached its firewall gateway |
| Routing | Static routes, OSPF process 1/Area 0, router IDs, WAN network advertisements, neighbor checks | Practiced; encountered duplicate router IDs and missing/wrong OSPF network statements |
| Firewall zoning | Trust, Untrust and Local zones, zone-based security policies, default deny | Practiced and inspected live policy output |
| Security policies | Permit LAN flows and IKE/ESP peer traffic; custom service object for UDP 500/4500; ICMP diagnostics | Firewall-A output showed VPN-LAN-OUT, VPN-PEER-IN, VPN-PEER-OUT and default deny; VPN-LAN-IN was missing in that snapshot |
| NAT | Source/destination NAT and related Huawei NAT concepts | Studied in course materials; no verified end-to-end execution evidence in this journal |
| High availability (Lab 5) | HRP heartbeat, VRRP virtual gateway, active/standby behavior and failover | Studied; currently beginning a new independent HA mock; no fresh completion evidence yet |
| User authentication (Lab 7) | Firewall-mediated employee/guest authentication and access-control practice | Covered in guided lab study; exact independent verification not preserved here |
| Site-to-site IPsec (Lab 8) | Interesting-traffic ACL 3000, IPsec ESP proposal, IKE proposal and peer, IPsec policy on WAN, IKE/IPsec SA inspection | One earlier guided attempt showed established SAs and encrypted/decrypted counters; later independent attempt reached IKE negotiation but not an established IPsec SA |

## Lab 8 — Site-to-site IPsec VPN

### Example lab topology

```text
PC1 -- FW-A -- AR1 -- FW-B -- PC2
10.1.1.0/24   40.1.1.0/30  40.1.1.4/30   10.1.2.0/24
```

- FW-A Trust: `10.1.1.1/24`; WAN: `40.1.1.1/30`
- AR1 WAN interfaces: `40.1.1.2/30` and `40.1.1.5/30`
- FW-B WAN: `40.1.1.6/30`; Trust: `10.1.2.1/24`
- PC1: `10.1.1.10/24`; PC2: `10.1.2.10/24`

### Configuration concepts

1. Establish interface addressing and reachability.
2. Configure OSPF on transit links and static routes for the remote LANs.
3. Apply firewall security policies for LAN-to-LAN traffic and IKE/ESP negotiation.
4. Match traffic selectors using mirrored advanced ACL 3000 rules.
5. Create an ESP tunnel proposal using AES-256 and SHA2-256.
6. Configure IKE proposal parameters, Diffie–Hellman group 14 and a pre-shared-key peer (key **not** recorded in this public repository).
7. Bind the IKE peer, proposal and ACL to an IPsec policy and apply it to the WAN interface.
8. Generate test traffic and inspect `display ike sa`, `display ipsec sa` and `display ipsec statistics`.

### Observed outcomes and troubleshooting

- **Earlier guided run:** IKE/IPsec security associations were established, and encryption/decryption counters increased (previously observed approximately 9 encrypted and 8 decrypted packets).
- **Independent repeat:** `display ike sa` showed one peer `40.1.1.6:500` in `NEG|A` (negotiating) state, not `RD` (ready). `display ipsec sa` returned no established SA.
- **Firewall-A policy snapshot:** `VPN-LAN-OUT` had 5 hits, `VPN-PEER-OUT` had 1 hit, `VPN-PEER-IN` had 0 hits, and default deny had 15 hits. This suggests traffic was being denied and/or peer negotiations were not matching expected rules; it does **not** by itself prove the root cause.
- **Peer rules checked:** Both firewalls had peer-in rules permitting IKE service and ESP from the opposite WAN IP to the local WAN IP.
- **Connectivity isolation:** A ping toward FW-B worked from AR1, while a firewall-originated WAN ping failed at one stage. This highlighted the difference between network reachability and firewall Local-zone policy permission.
- **Routing mistakes encountered:** Duplicate OSPF router IDs, an omitted transit network statement, and a static route with the wrong next hop. These were identified for correction; full final route verification was not preserved.
- **VRP syntax lesson:** A new IPsec policy needs its mode specified at creation (e.g., ISAKMP); attempting to create only a name and sequence generated a mode-required error.

## Lab 5 — Firewall high availability

Concepts being consolidated:

- Separate Trust, Untrust and HRP heartbeat networks.
- Configure HA peer communication and VRRP virtual gateways.
- Understand Active/Standby roles, synchronization and failover.
- Verify interfaces and HA state before attempting failover tests.

**Current independent mock:** Step 1/46 is in progress: address two HA firewalls' Trust, Untrust and heartbeat interfaces. No successful completion has yet been reported.

## Lab 7 — Authentication and access control

The current combined mock includes a dedicated firewall authentication/access-control section for employee and guest clients. The detailed worksheet and a verified output transcript are not available in this entry, so implementation-specific claims are intentionally limited.

## Troubleshooting workflow learned

1. Check physical link and `display ip interface brief`.
2. Test the directly connected default gateway before remote endpoints.
3. Inspect routing and OSPF neighbor state.
4. Inspect security policy rules and hit counters.
5. Verify that Local-to-Untrust and Untrust-to-Local permissions match the actual source/destination.
6. Inspect IKE phase state before expecting an IPsec SA.
7. Confirm bidirectional encrypted/decrypted counters before declaring the VPN operational.
8. Save configurations and preserve sanitized evidence.

## Next steps

- Finish the combined Lab 5 + Lab 7 + Lab 8 independent practical mock.
- Capture sanitized CLI outputs for HA state, authentication behavior, IKE/IPsec SAs and connectivity.
- Update this journal with verified outcomes and screenshots only after tests pass.

> This document separates **course study**, **guided practice**, and **verified outputs**. No live passwords, pre-shared keys or private institutional information are included.
