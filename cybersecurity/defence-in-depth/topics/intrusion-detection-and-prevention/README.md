# Intrusion Detection and Intrusion Prevention

**Evidence:** lectures and quiz discussions. Configuration syntax is educational; no alert, drop or actual sensor output has been independently authenticated.

## Architecture: detection versus prevention

A **network IDS** passively analyzes a copy of traffic through a network TAP or switch **SPAN** session; it alerts but generally cannot stop the original trigger packet. A **network IPS** is inline: inspected packets traverse the sensor, so it can drop or reset flows immediately. A **host-based** control observes a host's system activity; a network sensor sees only traffic traversing its observation point. IDS failure usually does not interrupt traffic; IPS overload, failure or misclassification may affect availability. IPS can normalize streams against evasion, while passive visibility may miss packets, asymmetrical traffic or encrypted payload content. Both require tuning.

**SPAN diagram in words:** two production endpoints exchange packets through a switch; a monitor session copies source-port/VLAN traffic to a dedicated destination port attached to the IDS. Only the copy reaches the sensor. The lecture uses `monitor session` for source/destination association and `show monitor` for verification:
```cisco
! Illustrative switch syntax only; ports are placeholders.
monitor session 1 source interface GigabitEthernet0/1 both
monitor session 1 destination interface GigabitEthernet0/2
! Verify in privileged EXEC:
show monitor session 1
```
A destination SPAN port should not be treated like a normal end-user access interface; validate switch platform behavior and whether oversubscription drops monitored frames.

## Signatures, micro-engines and detection approaches

A **signature** combines **type** (what malicious behaviour), **trigger/alarm** (matching event) and **action** (alert/drop/reset etc.). **Atomic** signatures inspect a single packet/activity; **composite** signatures correlate sequences/events across time or hosts. Cisco IOS micro-engines presented in the deck: **Atomic** (simple packet), **Service** (service-aware inspection), **String** (regular-expression content), **Multi-string** (flexible multiple patterns) and **Other** (miscellaneous processing). A signature hit is a lead for investigation, not automatic proof of compromise.

**Pattern-based** matches known characteristics; **anomaly-based** compares current traffic with a baseline of expected behaviour; **policy-based** identifies rule violations; **honeypot-based** deploys attractive decoy services to collect indicators and expose otherwise unseen activity. **Zero-day** threats have no known or widely deployed signature at discovery time, so pattern-only detection has a coverage gap. Reputation/global correlation and **Secure Device Event Exchange (SDEE)** are included as course-era approaches for sharing security events; availability depends on platform/release.

| Outcome | Actual activity | Alert result | Significance |
| --- | --- | --- | --- |
| True positive | Malicious | Alert | Detection worked |
| False positive | Benign | Alert | Noise and possible disruption |
| True negative | Benign | No alert | Benign activity handled correctly |
| False negative | Malicious | No alert | Missed detection |

Tuning means examining threshold, signature fidelity, environment and business traffic before enabling disruptive response. Alarm volumes must be evaluated against traffic baseline, missed events and operational cost.

## Cisco IOS IPS configuration lifecycle

The lecture sequence is: obtain supported IPS files → create a Flash configuration directory → install/verify appropriate crypto key → enable the IPS rule and interface inspection → load a compatible signature package → tune signature categories/actions → inspect logs/alerts. Each step has a failure mode: incompatible image, insufficient flash/memory, invalid signed package, rule not assigned or signatures still retired. **Retired** signatures are not participating in inspection; `retired true` applied to `all` followed by `retired false` for the `ios_ips basic` category selects a smaller active set.

**Illustrative category-selection excerpt from the studied command pattern:**
```cisco
ip ips signature-category
 category all
  retired true
 exit
 category ios_ips basic
  retired false
 exit
```
Exact parser prompts, activation/commit steps, packages and storage layout are image-specific. Do not claim this ran successfully based on an assessment question. An IPS test needs redacted running configuration, loaded signature status, safe authorized test traffic, signature/event identifier and observed allowed-versus-dropped packet outcomes. Alert delivery alone cannot demonstrate a packet was blocked.

**What I learned:** monitoring visibility and on-path prevention have different fault models; signature engineering balances missed detections against false alarms; detection is layered with firewall controls and host telemetry. **Not verified:** working SPAN, installed IPS package, signature hits or dropped attacks. See [practical exercise register](../../PRACTICAL_EVIDENCE.md).
