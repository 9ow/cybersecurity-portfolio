# Firewall High Availability

**Source:** `Firewall Hot Standby Technologies.pptx`. Provisional placement under Week 6, not verified as studied or practised.

## Failure tolerance and VRRP
- Two border firewalls avoid single-point-of-failure. **VRRP (Virtual Router Redundancy Protocol)** gives a virtual default gateway; **Master** owns forwarding, **Backup** takes over after failure and sends gratuitous ARP.
- VRRP priority in PPT **0–255**, higher wins, tie broken by higher interface IP. Multiple zones need coordinated VRRP groups; asymmetric return path can fail stateful inspection.

## VGMP
- **VRRP Group Management Protocol (VGMP)** manages multiple VRRP groups as one unit.
- States: **initialize** (not enabled), **load-balance** (equal priority), **active** (higher priority), **standby** (lower).
- VGMP/HRP packets via heartbeat link; default Hello interval **1 second**. Manages VRRP status consistency and preemption.

## HRP
- **Huawei Redundancy Protocol** synchronizes configurations and dynamic state (sessions and mapping tables). Active/standby: active processes traffic and replicates; load balancing: both process and replicate.
- **Automatic backup** default; manual batch and quick-session options; static-route synchronization requires `hrp auto-sync config static-route`.
- Heartbeat interfaces physical GE or logical Eth-Trunk, five states: **Invalid, Down, Peerdown, Ready, Running**.
- Fault cases: service line, whole firewall, heartbeat link (possible dual-active). Missing five HRP Hello intervals triggers failover. Preemption is enabled by default; delay **60 seconds**.

## PPT CLI configuration examples
```text
[FWA-10GE0/0/1] vrrp vrid 1 virtual-ip 1.1.1.1 active
[FWB-10GE0/0/1] vrrp vrid 1 virtual-ip 1.1.1.1 standby
[FWA-10GE0/0/3] vrrp vrid 2 virtual-ip 10.3.0.3 active
[FWB-10GE0/0/3] vrrp vrid 2 virtual-ip 10.3.0.3 standby
[FWA] hrp interface 10ge0/0/7 remote 10.10.0.2
[FWB] hrp interface 10ge0/0/7 remote 10.10.0.1
[FWA] hrp enable
[FWB] hrp enable
```
The lecture also contains HRP authentication-key configuration; literal password intentionally excluded from repository notes. No command claimed to have been run.
