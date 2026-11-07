# Practical Security Learning — Evidence-First Portfolio

This section connects four academic learning tracks to independently reproducible, authorized exercises. It is a **learning roadmap**, not a claim that every exercise has been completed. No current/in-progress university group project, private HomeLab deployment, raw coursework technical materials, student identifiers, or private infrastructure details are included.

## Ethical Hacking — authorized assessment methodology
- **Reconnaissance and scoping:** define written authorization, permitted target ranges, time window and exclusions before testing.
- **Service discovery:** compare TCP SYN probes, completed handshakes, closed/filtered results and application banners; distinguish observations from inferred vulnerabilities.
- **Enumeration:** interpret DNS, SNMP, LDAP, SMTP and FTP responses in deliberately configured practice targets.
- **Vulnerability assessment:** record CVE, affected version, evidence, severity rationale and remediation; do not infer exploitability from a port alone.
- **Suggested deliverable:** sanitized service-discovery matrix and an assessment report with scope, evidence, false positives and limitations.
- **Evidence status:** course concepts documented; personal execution must be independently demonstrated.

## Defence in Depth — preventive and detective controls
- **Identity and administration:** SSH management, AAA authentication/authorization/accounting, least privilege and fallback behavior.
- **Segmentation:** VLAN boundaries, extended ACL rule order and stateful firewall/zone-policy directionality.
- **Network detection:** SPAN traffic visibility, IDS/IPS alerts, signature tuning and benign/malicious test distinctions.
- **Layer 2 safeguards:** port security, DHCP snooping and Dynamic ARP Inspection.
- **Suggested deliverable:** control matrix with threat, configuration objective, positive/negative test, observed output and residual risk.
- **Evidence status:** study notes and unverified practical exercise plans; do not mark tests passed without captured results.

## Enterprise Network Security — Huawei
- **VRP operations:** interface, routing, service and management-plane inspection.
- **Firewall policy:** security zones, policy order, session state, default-deny and ASPF behavior.
- **Address translation:** source/destination NAT, NAPT, Easy IP and NAT Server; distinguish reachability from policy authorization.
- **Resilience:** VRRP, VGMP, HRP and failover verification, with explicit device/software compatibility.
- **Suggested deliverable:** sanitized policy matrix, packet-path explanation and command/output verification register.
- **Evidence status:** reference knowledge; Huawei practical exercise execution is not yet independently verified.

## Artificial Intelligence and Data Analysis
- **Python data workflow:** load a non-sensitive dataset, validate schema, handle missing values and encode features.
- **Modeling:** create train/test split, baseline classifier and reproducible scikit-learn pipeline; avoid data leakage.
- **Evaluation:** confusion matrix, precision, recall, F1 and class imbalance; explain why accuracy alone can mislead.
- **Security application idea:** on a synthetic dataset, evaluate whether flow-derived features can assist triage; distinguish a model's predictions from validated incident findings.
- **Suggested deliverable:** runnable notebook, sanitized sample data, dependency versions, reproducible metrics and model limitations.
- **Evidence status:** topic documentation; no claim of a completed model experiment without executable code and outputs.

## Reusable evidence checklist
1. Objective and authorized scope.
2. Environment described without private topology, credentials or real host details.
3. Exact procedure actually performed (not a lecture example).
4. Expected versus observed outcome with timestamped, redacted output.
5. Interpretation, alternative explanations and limitations.
6. Troubleshooting, remediation and retest if applicable.

**Publication boundary:** This is original learning-oriented synthesis, not redistributed lecture technical materials or current assessed-project work. Planned exercises remain labeled planned until independently verified.
