# Intro to LAN — TryHackMe

**Status:** Completed | **Focus:** LAN design, IPv4 subnetting, ARP, DHCP, and network security fundamentals

## Overview
This technical note documents the networking concepts studied in TryHackMe's *Intro to LAN* room. The emphasis is on how local networks are structured, how devices discover their neighbours, and how hosts receive network configuration. The diagrams and addresses below are illustrative rather than collected from a private network.

## 1. LAN topologies

| Topology | Structure | Advantages | Limitations |
| --- | --- | --- | --- |
| Star | End devices connect to a central switch or hub | Easy to expand; an individual endpoint failure generally stays local | More cabling; the central device is a single point of failure |
| Bus | Devices share a backbone cable | Simple and inexpensive | Shared-medium congestion and backbone failure risk |
| Ring | Devices form a closed loop | Predictable forwarding path in a basic ring | A single broken connection/device can disrupt a simple unprotected ring |

A **single point of failure (SPOF)** is a component whose failure can interrupt a service or network. Redundant links and equipment can improve availability, but must be designed and configured correctly.

### Switch versus router
- **Switch:** primarily forwards Ethernet frames within a LAN using learned MAC-to-port mappings. Unknown unicast and broadcast frames may be flooded within the relevant VLAN.
- **Router:** forwards IP packets between distinct networks based on routing information. A host normally sends off-subnet traffic to its default gateway.

## 2. IPv4 subnetting

Subnetting divides an address block into smaller networks for administration, broadcast-domain design, and policy enforcement.

Example host configuration:

```text
Host IP:           192.168.1.100
Prefix:            /24
Subnet mask:       255.255.255.0
Network address:   192.168.1.0
Usable hosts:      192.168.1.1 - 192.168.1.254
Broadcast address: 192.168.1.255
Gateway example:   192.168.1.254
```

The network address identifies the subnet; a host address identifies an interface within it; a **default gateway** is the next-hop device used to reach other networks. The gateway address is not inherently fixed to `.1` or `.254`: it must be configured on an appropriate router interface.

### Segmentation example
A café can separate staff systems (e.g., point-of-sale terminals) from customer Wi-Fi using distinct IP subnets and appropriate VLANs or other separation mechanisms. **Different subnets alone are not an access-control policy**: routing controls, ACLs, or firewall rules are needed to restrict guest access to staff resources while allowing intended internet access.

## 3. Address Resolution Protocol (ARP)

ARP resolves an IPv4 address to a link-layer MAC address on the local network.

1. A host checks its **ARP cache** for an existing mapping.
2. If none is available, it sends a broadcast **ARP Request** asking who owns the target IPv4 address.
3. The target typically returns a unicast **ARP Reply** containing its MAC address.
4. The requester caches the mapping for subsequent Ethernet delivery.

Illustrative exchange:

```text
PC-A (192.168.1.10): Who has 192.168.1.20? Tell 192.168.1.10
PC-B (192.168.1.20): 192.168.1.20 is at AA:BB:CC:11:22:33
```

For a remote destination, the sender typically resolves the **next-hop gateway's** MAC address rather than the remote host's MAC. IPv6 uses Neighbor Discovery instead of ARP.

**Security consideration:** ARP spoofing/poisoning can mislead hosts about IP-to-MAC mappings and potentially enable traffic interception or disruption. Appropriate network controls and monitoring reduce exposure.

## 4. Dynamic Host Configuration Protocol (DHCP)

DHCP automates IPv4 network configuration, often providing an address, subnet mask, default gateway, and DNS server. The initial exchange is remembered as **DORA**:

| Step | Message | Direction | Purpose |
| --- | --- | --- | --- |
| 1 | Discover | Client → network | Find available DHCP servers |
| 2 | Offer | Server → client | Propose an address and configuration |
| 3 | Request | Client → server | Request the offered lease |
| 4 | ACK | Server → client | Confirm the lease |

A DHCP address is commonly **leased for a period**, not necessarily assigned permanently.

**Security consideration:** An unauthorized (rogue) DHCP server could provide incorrect network settings, including a malicious gateway. DHCP snooping is one defensive feature available on suitable switches.

## 5. Key distinctions

- **Network address** identifies the subnet; **host address** identifies an interface within it.
- **Default gateway** provides a path to other networks.
- **ARP Request** asks for an IPv4-to-MAC mapping; **ARP Reply** supplies it.
- **DHCP Discover/Offer/Request/ACK** negotiates an address lease.
- **Subnetting** organizes IP space; **segmentation enforcement** requires suitable network policy.

## Learning outcome
Completed the Intro to LAN room and reviewed topology failure modes, switch/router roles, subnet address types, ARP discovery and caching, and the DHCP DORA process. This write-up is a conceptual record; it does not claim independent packet-capture evidence or deployment of network controls.

**Source:** [TryHackMe — Intro to LAN](https://tryhackme.com/room/introtolan)
