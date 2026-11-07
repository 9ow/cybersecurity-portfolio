# Cisco Network Device Hardening and Management

**Evidence:** lecture-derived explanations and illustrative IOS syntax; no device-output verification is supplied.

## Protection strategy and administrative paths

A router has physical, operating-system/configuration and service attack surfaces. Lock equipment in controlled rooms, restrict consoles and removable media, maintain tested backups and controlled software images, keep software patched, disable unneeded services, log changes and review management permissions. Edge architectures in the slides compare a single edge router, multiple layered controls and a **DMZ** isolating public-facing servers. Isolation limits blast radius; an edge router alone cannot establish trust.

**Local console** is physically attached; **AUX/modem** is an alternate management path; **VTY** lines accept remote CLI sessions; a **dedicated OOB management network** separates administrative traffic from production. In-band management is convenient from multiple sites and tools but requires restrictive routing/ACLs and encryption. OOB offers a recovery channel if production forwarding is broken and reduces exposure of management protocols on user networks. Both still require authorization.

## Secure passwords, line controls and SSH

The source distinguishes reversible IOS **Type 7** obfuscation from stronger secret hashes, including Type 8/9 where supported. The historical lecture encourages long, unique, non-obvious passwords and minimum length; policy should also consider secure storage and resistant login flows. `service password-encryption` is **not** a substitute for a one-way password hash.

**Illustrative configuration only (not executed):**
```cisco
hostname LAB-RTR
ip domain-name example.invalid
security passwords min-length 10
! Configure local usernames and secrets interactively; do not commit them.
service password-encryption
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 4
 login local
 transport input ssh
 exec-timeout 3 30
!
login block-for 120 attempts 3 within 60
login on-failure log
```
The hostname/domain and RSA key generation are SSH prerequisites on common IOS images; `ip ssh version 2` selects the safer version. `transport input ssh` excludes Telnet. `exec-timeout 3 30` disconnects an idle session after 3 minutes 30 seconds. `login block-for` rate-limits repeated failures, but badly chosen thresholds can deny legitimate administrators. `login quiet-mode access-class` can exempt designated administrative sources during a quiet period; apply it deliberately to avoid lockout. `show login failures` provides diagnostic evidence without displaying credentials.

A legal banner, controlled `enable` access and login logging support accountability. SSH encrypts the management session; it does not decide which commands an authenticated user is authorized to perform.

## Least-privilege command access

Cisco IOS **privilege 1** is normal user EXEC and **15** is privileged EXEC. Levels 2–14 can be assigned commands but inherit lower-level commands; coarse hierarchy and multi-keyword command handling limit precision. **Root view** manages Role-Based CLI views; a **CLI view** exposes a chosen command set; a **superview** aggregates views and cannot contain commands directly. A security operator might need inspection, log and firewall commands; a network engineer might need interface and routing commands. Test allowed commands *and* rejected commands, because showing a parser-view configuration alone does not prove access restrictions.

## Operational telemetry and reliable time

**Syslog** may be delivered to console, VTY monitor, local buffer or remote collector. Lower severity number means more urgent: 0 emergency, 1 alert, 2 critical, 3 error, 4 warning, 5 notice, 6 informational, 7 debugging. An illustrative `logging host 192.0.2.50` targets a reserved documentation host; `logging trap warnings` chooses remote severity threshold. `show logging` verifies configured destinations and counters. Do not mistake a logged attempt for a successful denial until traffic tests confirm it.

**SNMP:** a manager queries an agent on a managed node; **GET** reads, **SET** changes and **TRAP** pushes events. The lecture contrasts weak v1/v2c community-based controls with SNMPv3 authentication, integrity, encryption and access control; **authPriv** provides authenticated, encrypted management when correctly configured. Restrict management stations and views; `show snmp user` helps verify users without exposing secrets.

**NTP** synchronizes device clocks so distributed syslog and AAA events can be correlated. The lecture covers an NTP server, authenticated time source and `ntp trusted-key`; `show ntp associations` and `show ntp status` indicate peers and synchronization. Authentication protects acceptance of an approved time source; it is not a substitute for reliable clock and source selection.

## Routing integrity and resilient configuration

Routing-protocol spoofing can redirect, blackhole or loop traffic. OSPF interface authentication (legacy MD5 and SHA/key-chain mechanisms in supported images) protects routing adjacencies against unauthorized peers; matching algorithm/key-id/key material and platform support matter. **CoPP** protects CPU-bound protocol traffic by matching classes and policing, not by blocking packets already forwarded through the data plane. **IOS resilient configuration** (e.g., `secure boot-image` and `secure boot-config` in compatible releases) helps protect an IOS image/configuration and can change normal `dir` visibility; confirm restore procedures in a safe environment.

**What I learned:** availability of a secure management channel, secure identity, least privilege and trustworthy logs are separate requirements. **Not verified:** SSH session outcomes, log delivery, privilege-view enforcement, OSPF adjacency, NTP synchronization or protected-image recovery. See [lab register](../../LAB_EVIDENCE.md).
