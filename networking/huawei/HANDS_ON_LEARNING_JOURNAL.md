# Huawei Enterprise Network Security — Learning Journal

**Platform:** Huawei eNSP, VRP, USG firewalls  
**Focus:** Enterprise networking, firewall security, high availability, authentication and secure site-to-site connectivity

## Topics covered

| Topic | Skills and concepts |
|---|---|
| VRP device management | User and system views, interface configuration, device inspection, saving configurations |
| Network connectivity | IPv4 addressing, subnet masks, default gateways, ping, interface status |
| Routing | Static routes, OSPF Area 0, router IDs, WAN advertisements, neighbor verification |
| Firewall zones | Trust, Untrust, Local and DMZ, zone assignments, traffic direction |
| Security policies | Source/destination zones and addresses, service objects, rule matching, default deny, session inspection |
| Network address translation | Source NAT, NAT Server, address pools and policy-based translation |
| High availability | HRP, VRRP, active/standby roles, heartbeat interfaces, synchronization and failover |
| Authentication | User access control, guest access, authentication exemption and portal-related configuration |
| IPsec VPN | Advanced ACL traffic selection, IKE peers and proposals, ESP tunnel mode, IPsec policies and security associations |

## VRP and network configuration

Huawei VRP uses different CLI views for device-wide and interface-specific configuration. Key operational habits include checking interface status, verifying addressing, testing the nearest gateway before distant destinations, and saving the running configuration.

Routing practice covers static next hops and OSPF on WAN links. Router IDs must be unique, and each router must advertise the intended connected network.

## Firewall security and NAT

Security zones determine the direction of traffic inspected by Huawei USG policies. A rule can match source zone, destination zone, source and destination addresses, and services. The default-deny rule blocks traffic that does not match a permit policy.

NAT concepts include source translation for outbound traffic and NAT Server for publishing selected services. Access permission and address translation are separate configuration decisions.

## High availability: HRP and VRRP

A redundant firewall pair uses a dedicated heartbeat connection and coordinated active/standby behavior. VRRP provides virtual gateway addresses; HRP supports state and configuration synchronization. During a controlled failover, the standby firewall should assume forwarding responsibility, subject to correct configuration and network health.

Useful checks include `display hrp state`, `display vrrp brief`, security-policy inspection and connectivity testing.

## User authentication and guest access

Firewall access control can combine security policies with authentication behavior. Guest traffic may be exempted from authentication for specifically permitted services, while other users can be subject to configured authentication requirements.

Authentication rules and security policies serve different purposes and both should be checked when access does not work as expected.

## Site-to-site IPsec VPN

A site-to-site VPN connects two private networks through an untrusted WAN. Typical configuration sequence:

1. Configure firewall and router IP addresses and verify local connectivity.
2. Establish WAN routing using OSPF and/or static routes as required.
3. Permit IKE, ESP and the intended intersite traffic with firewall security policies.
4. Use mirrored advanced ACLs to identify protected traffic.
5. Define an ESP tunnel proposal with AES-256 encryption and SHA2-256 authentication.
6. Configure IKE proposal settings, Diffie–Hellman group 14 and matching peer parameters.
7. Create an IPsec policy, reference the ACL, IKE peer and ESP proposal, then apply it to the WAN interface.
8. Generate intersite traffic and inspect `display ike sa`, `display ipsec sa` and `display ipsec statistics`.

### Troubleshooting lessons

- An IKE association showing `NEG` is still negotiating; it is not equivalent to a ready tunnel.
- No output from `display ipsec sa` means an active IPsec SA has not been confirmed.
- A successful ping from a transit router does not automatically mean a firewall-originated ping will be permitted.
- Firewall Local-to-Untrust and Untrust-to-Local rules can affect IKE and diagnostic traffic.
- Policy hit counters help narrow down traffic matching, but do not establish a root cause on their own.
- Incorrect OSPF router IDs, missing network statements and wrong static next hops can disrupt reachability.
- An IPsec policy requires a creation mode such as ISAKMP when the policy/sequence combination is new.

## Practical checklist

- [ ] Inspect interfaces and IP addresses
- [ ] Confirm default gateways and routing
- [ ] Verify security zones and policy matches
- [ ] Check authentication and NAT rules where relevant
- [ ] Inspect HRP/VRRP state for redundant firewalls
- [ ] Verify IKE/IPsec associations for encrypted site-to-site connectivity
- [ ] Save configurations after testing

*Personal technical study notes for Huawei enterprise network security.*
