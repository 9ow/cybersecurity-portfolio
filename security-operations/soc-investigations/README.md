# SOC Investigation — Service Discovery in a Synthetic Network Dataset

**Practice area:** Detection triage, network evidence analysis, alert correlation and structured incident reporting.  
**Investigation type:** TCP SYN port diversity / service discovery.  
**Evidence:** Synthetic PCAP data processed into Suricata flows and alerts, and a separate simulated host-note record.  
**Disposition:** Preliminary assessment; exercise authorization has not been independently established.

## Investigation objective
Assess a series of TCP SYN attempts from a simulated scanner to a simulated target, determine whether the underlying observations support service discovery and evaluate an alternative explanation that the activity was an approved inventory exercise.

The dataset is **simulated**, not a network capture from a private HomeLab or a production environment.

## Observed evidence

| Evidence type | Observation | Interpretation |
| --- | --- | --- |
| TCP flow record A | One outbound SYN toward destination port **80** | A connection attempt, not proof of an HTTP session |
| TCP flow record B | One outbound SYN toward destination port **443** | A second observed destination service/port |
| Suricata alert | SYN-burst pattern with destination port **139**; lab signature **SID 1000002** | Alert correlates with multiple SYN attempts; the SID alone does not establish port diversity |
| Synthetic host note | Label: **Authorized inventory exercise** | Plausible benign explanation; not independently verified permission |

### Timeline reasoning
The flows and alert belong to the same short burst; their timestamps were normalized to **UTC** because an alert used a timezone offset while other logs were already in UTC. The reviewed sample contains **at least three distinct destination ports** (80, 443 and 139); full-port cardinality for the case has not been established.

## Technical analysis

### Distinguishing scanning from connection success
The examined flow examples contained TCP `SYN` flags and a single observed packet in the client-to-server direction with no corresponding response packet in those records. This supports **connection attempts**, but does not prove that a remote service was unavailable, a three-way handshake completed, or any host was compromised.

### Signature versus corroborating evidence
A detection rule with SID `1000002` reported a SYN-burst pattern. The signature name is a clue, but the analyst independently checked the destination-port fields in raw flow records. **An alert ID does not encode how many unique ports were attempted.**

### Alert disposition and severity
The Suricata event indicated `action: allowed`: it reported the behavior without demonstrating an enforcement block. A signature priority value does **not** prove real-world business impact or a successful connection.

### Authorization and competing explanations
The accompanying synthetic note described an inventory exercise. Its time and associated simulated source matched the investigation closely enough to form a hypothesis, but a note alone cannot prove an approved change ticket, schedule, scoped targets or responsible asset owner. An unrelated routine host-health note was not treated as evidence of the same event merely because its timestamp was close.

## Working assessment
**Observed:** SYN-based behavior across multiple destination ports consistent with service discovery.

**Not established:** Malicious intent, full handshake, exploitation, compromise, validated business impact, or independent authorization.

**Alternative explanation:** Scheduled inventory/maintenance scan. If a scan is both observed and later confirmed legitimate, a **benign true positive** may be more accurate than labeling the detection a false positive.

## Response and next validation
1. Determine the full distinct-port set using the relevant original synthetic flows, not a duplicated count of imported alert rows.
2. Validate claimed inventory authorization against an approved schedule, scope and responsible asset owner.
3. Seek any additional relevant response traffic and endpoint context before concluding that a connection or exploit succeeded.
4. Document impact, uncertainties, recommendation and final disposition before closing the case.
5. Treat containment as proportional to verified risk, rather than isolating a device solely because a signature matched.

## Technical skills demonstrated
- Suricata rule and flow interpretation
- Raw JSON inspection and event correlation
- TCP SYN/flag and packet-direction reasoning
- UTC timestamp normalization and evidence timelines
- Hypothesis testing and authorization context
- False-positive versus benign-true-positive classification
- SOC case narrative and incident-report recommendations

## Disclosure boundary
No real/private HomeLab IPs, hostnames, management URLs, topology, access commands, software deployment information or raw logs are included. This case uses synthetic training data only and must not be interpreted as evidence of a real intrusion.
