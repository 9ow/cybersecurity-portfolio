# Nmap: discovery, transport scans and evidence interpretation

Nmap is a network reconnaissance and service fingerprinting utility. These examples use `<AUTHORIZED_HOST>` and `<AUTHORIZED_SUBNET>` placeholders; commands require a separately approved target and rules of engagement. This document explains behavior, not a record of execution.

## Assessment sequence and decision points

1. Confirm asset ownership, IP allocation, maintenance window, excluded subnets, rate and acceptable traffic.
2. Discover responsive assets with `nmap -sn <AUTHORIZED_SUBNET>`. Read the result as responsive to the chosen discovery probes, not a complete inventory. On local Ethernet, ARP/neighbor discovery can return devices even if ICMP echo is blocked.
3. Choose a small service subset (`-p 22,80,443`), then expand where justified; avoid flooding sensitive devices.
4. Identify reported service and version with `-sV`, then evaluate whether banners and fingerprints are trustworthy.
5. Use specific, reviewed NSE scripts for the services found, preserve machine-readable output and independently validate findings.
6. Produce prioritized recommendations; record what could not be tested and why.

## TCP state and scanning mechanics

The TCP three-way handshake is SYN from client, SYN/ACK from an accepting server, then ACK from the client. A RST resets a connection. FIN requests orderly close; PSH and URG are data-handling flags. NULL means a probe has no TCP control flags.

| Option | Probe behavior | Key interpretation | Limitations |
|---|---|---|---|
| `-sT` | OS creates full TCP connection | Connect succeeds: likely open; refusal: closed | Easily logged by target services; can be used without raw-packet privileges |
| `-sS` | Sends SYN, does not finish the ordinary connection | SYN/ACK indicates open; RST indicates closed; silence or relevant ICMP error indicates filtering | Requires raw packet privileges in many environments; not invisible to network monitoring |
| `-sF` | FIN-only packet | RST indicates closed; silence means open**or**filtered | Nonstandard response behavior on operating systems |
| `-sN` | No TCP flags set | RST indicates closed; silence means open**or**filtered | Modern firewalls and Windows behavior make this ambiguous |
| `-sX` | FIN/PSH/URG flags | Similar closed versus open/filtered logic | Does not establish an application connection |
| `-sA` | ACK probe | RST generally means unfiltered; silence/ICMP may mean filtered | Cannot tell open from closed |
| `-sU` | UDP datagram; may use service-aware payloads | UDP reply indicates open; ICMP type 3/code 3 closed; silence is often open|filtered | ICMP throttling, filtering, no handshake and application-specific response are common ambiguities |

A port with `open` status is an observation, not proof of a vulnerability. `closed` means reachable yet no accepting socket by that method. `filtered` means filtering or packet loss prevented reliable determination. `open|filtered` and `closed|filtered` are explicitly uncertain classes. When a UDP probe is silent, do **not** write that the port is confirmed open.

## Hosts, protocols and selection

| Syntax | Purpose / operational consideration |
|---|---|
| `nmap <AUTHORIZED_HOST>` | Default scan of a host, commonly the most popular 1,000 TCP ports |
| `nmap <AUTHORIZED_SUBNET>` | Scans a CIDR range: every address must be authorized |
| `nmap -iL targets.txt` | Read target list; inspect list for unexpected addresses and duplicates first |
| `nmap -p 80,443 <AUTHORIZED_HOST>` | Only specified ports |
| `nmap -p 20-23 <AUTHORIZED_HOST>` | Inclusive range |
| `nmap -p- <AUTHORIZED_HOST>` | All TCP ports (1–65535); may increase time and traffic |
| `nmap -sU -p 53,161 <AUTHORIZED_HOST>` | Targeted UDP checks, often slower |
| `nmap -sS -sU -p T:22,U:53 <AUTHORIZED_HOST>` | Explicit TCP and UDP selection |
| `nmap -6 <AUTHORIZED_IPV6>` | IPv6 target and IPv6 scanning path |

A `/24` represents a prefix length, not intrinsically a historical “class C” network. Hostnames may resolve to multiple addresses and change during an assessment.

## Discovery vs port scanning

`-sn` performs host discovery without a subsequent port scan (historically `-sP`). `-PE` sends ICMP echo probes; `-PS22,80` uses TCP SYN discovery against selected destination ports. `-Pn` skips the normal discovery decision and treats all specified addresses as candidates for port scanning—**not** “disable port discovery.” A missing ping reply does not mean a machine is powered off. Firewalls, transit controls, ARP/ND behavior and endpoint policy alter what is observed.

## Service, OS and topology identification

`-sV` sends additional probes and matches banners/protocol behavior against signatures. `-O` attempts TCP/IP stack fingerprinting and may require good open/closed-port conditions. `-A` combines OS identification, version probes, default scripts and traceroute. `-sC` executes default scripts (not automatically harmless on every environment). HTTP on port 8080, SSH on nonstandard ports and reverse proxies illustrate why port numbers alone are not product proof. TTL-based OS guesses are weak because hops modify TTL and initial values overlap.

Network diagrams should distinguish directly observed nodes/links from inferred subnets, gateways and paths. A traceroute hop missing a reply is not proof that a router does not exist.

## Performance, output and reproducibility

`-T0` through `-T5` change timing; the default is `-T3`. Slower timing may reduce traffic but cannot guarantee sensor avoidance. More aggressive timing may increase packet loss or false negatives. Use `--max-rate <RATE>` to cap probe sending rates; `--max-parallelism <COUNT>` bounds concurrent activity. `-v` shows more progress detail; `-V` shows installed version.

Output switches: `-oN report.nmap` human-readable; `-oX report.xml` structured; `-oG report.gnmap` legacy grepable; `-oA report` writes all three. Document Nmap version, flags, authorized scope, observation date/time, unresolved hosts, timeouts and uncertainty. Never publish raw infrastructure output.

## Common mistakes, troubleshooting and security implications

- Host marked down: verify discovery method, firewall and authorized `-Pn` comparison; do not assume offline.
- `open|filtered` on UDP or FIN/NULL/Xmas: classify as uncertain, follow up with an appropriate protocol-aware query.
- Slow or incomplete scan: reduce scope, check packet-loss/rate limit and scan authorization; record limitations instead of hiding them.
- Different results from `-sS` and `-sT`: routing, permissions, middleboxes and endpoint behavior may differ.
- Version name from a banner: compare with vendor information and actual configuration before claiming a CVE.
- Extremely broad script sets or fast parallel scans can disrupt fragile systems. Use only approved methods.
- A detection finding is valuable even when access is not demonstrated: exposed management services, unnecessary listeners and weak segmentation merit defensive investigation.

See also [NSE guide](nse-and-service-assessment.md) and [enumeration](protocol-enumeration.md). Reference: https://nmap.org/book/man.html.