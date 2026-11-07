# ACLs, Firewalls and Zone-Based Security Policies

**Evidence:** lecture-grounded reference plus clearly labelled illustrative IOS configuration. No captured packet tests, running policies or counters establish a working deployment.

## ACL semantics and architecture

An **Access Control Entry (ACE)** permits or denies packets; the ACL evaluates statements **top down**, stops at first match and otherwise reaches an **implicit deny**. A **standard ACL** primarily matches source IPv4 address, while an **extended ACL** matches protocol, source and destination IPv4 addresses and relevant TCP/UDP ports/flags. **Numbered** and **named** forms provide ways to define lists; names/sequence numbers and `remark` support maintenance. Interface `ip access-group NAME in|out` filters traffic entering/leaving that interface from the router's perspective. VTY `access-class` restricts management source access instead of general transit traffic. Placing a standard ACL near the destination reduces unintended source-wide impact; extended ACLs are typically close to source, balanced against topology and operational constraints.

**Wildcard masks invert a subnet mask.** For example a /27 mask `255.255.255.224` becomes `0.0.0.31`; a /20 becomes `0.0.15.255`. `host 192.0.2.10` is equivalent to `192.0.2.10 0.0.0.0`; `any` matches any address. Each wildcard 0 bit must match; each 1 bit is ignored. ACL statements are not evaluated like routing longest-prefix matches. Ordering is therefore critical.

**Illustrative policy:** deny HTTP (destination TCP/80) from documentation subnet A to one documentation server while permitting other traffic to documentation subnet B:
```cisco
ip access-list extended WEB_POLICY
 remark Specific denial precedes broader permission
 10 deny tcp 192.0.2.0 0.0.0.255 host 198.51.100.10 eq 80
 20 permit ip 192.0.2.0 0.0.0.255 198.51.100.0 0.0.0.255
 30 deny ip any any log
interface GigabitEthernet0/0
 ip access-group WEB_POLICY in
```
This illustrates rule selection, **not an executed practical exercise**. Rule 20 does not permit arbitrary other destinations, and logging an explicit final deny differs from relying silently on implicit denial. For a source-specific rule to work, the chosen interface and direction must actually see that source's ingress packets. To edit, remove or insert a specific sequence entry instead of adding a broad `permit any any` before restrictions. Verification would use `show access-lists`, `show ip interface`, match counters and positive/negative traffic tests.

## Firewall types, state and DMZ

**Stateless packet filters** inspect each packet's fields, often described by the source/destination IP, source/destination port and protocol **five-tuple**. They do **not** remember a session. A **stateful firewall** stores connection state (e.g. TCP handshake/session information) and can allow legitimate return traffic for outbound sessions. **Application gateways / proxies** process application semantics such as HTTP or FTP and can relay on behalf of clients; more inspection brings complexity and processing overhead. The technical materials also discuss NAT firewalls, which are **not** complete access control simply by hiding addresses.

A useful stateful-flow diagram would show an internal client initiating TCP to a permitted external service, creation of a state-table entry and related return packets matching that state; a new unsolicited inbound connection is a different flow and should be rejected. Firewalls must sit on the actual traffic path, resist attack and enforce policy. Their limitations include misconfiguration, encrypted payload visibility, insider threats, performance overhead and bypass paths.

**DMZ** architecture places exposed services on a separate segment between Internet and internal LAN; external clients may reach only explicitly published services, while DMZ-to-internal connections remain narrowly controlled. “Internal” does not mean automatically safe.

## Classic IOS firewall and CBAC

The **Classic Firewall / Context-Based Access Control (CBAC)** chapter selects internal/external interfaces, builds interface ACLs, defines `ip inspect` rules for permitted protocols and attaches inspection at the appropriate interface/direction. The state engine opens temporary return-flow permissions according to recognized sessions. This interface-oriented design requires careful ACL/inspection coordination and differs from zone-to-zone policy. **Conceptual syntax** (not validated on any IOS image):
```cisco
ip inspect name OUTBOUND http
interface GigabitEthernet0/0
 ip inspect OUTBOUND out
```

## Zone-Based Policy Firewall (ZPF)

The source defines **zones** as security boundaries and **directed zone pairs** as the path for traffic classification. **Class maps** identify protocol matches; **policy maps** choose an action; **service-policy** binds the policy to a zone pair; interface **zone-member security** assigns membership. A design sequence is: determine zones → requirements between zones → physical path → traffic classes and policies → apply and verify.

- **inspect:** stateful packet inspection; return traffic for the established session is permitted according to state.
- **pass:** allows matching traffic *without* session tracking; a reverse-direction policy may be required for return traffic.
- **drop:** blocks matching traffic and may be logged.

**Directional illustrative configuration** (adapt interfaces to the authorized practical exercise; no claim of execution):
```cisco
zone security INSIDE
zone security OUTSIDE
class-map type inspect match-any WEB_TRAFFIC
 match protocol http
 match protocol https
policy-map type inspect INSIDE_POLICY
 class type inspect WEB_TRAFFIC
  inspect
 class class-default
  drop
zone-pair security INSIDE_TO_OUT source INSIDE destination OUTSIDE
 service-policy type inspect INSIDE_POLICY
interface GigabitEthernet0/0
 zone-member security INSIDE
interface GigabitEthernet0/1
 zone-member security OUTSIDE
```
The direction **INSIDE → OUTSIDE** matters; this does not permit unsolicited OUTSIDE → INSIDE traffic. Between distinct security zones, traffic requires a policy; interfaces in the *same* zone can communicate by default. Traffic to/from the router's **self zone** has special rules and should be considered when protecting routing, DNS or management-plane sessions. Zone membership changes can disrupt existing traffic if applied prematurely: preserve console access and build classes/policies before moving live interfaces.

**Verification:** `show zone security`, `show zone-pair security`, `show class-map type inspect`, `show policy-map type inspect`, `show policy-map type inspect zone-pair sessions` and `show run | begin class-map`. Check source/destination, active session state, permitted TCP/80/443, blocked out-of-policy traffic and actual reverse flow. `inspect` cannot be proved from a static screenshot of policy text.

**What I learned:** ACL rule order and interface direction govern stateless enforcement; a ZPF is a directional policy system, and `inspect` differs fundamentally from `pass`. **Not verified:** ACL match counters, transit tests or ZPF session state. See [practical exercise register](../../PRACTICAL_EVIDENCE.md).
