# Reporting methodology and lab evidence integrity

Based on Unit 1 authorization ethics and Unit 3–5 scan-result interpretation; a methodology guide, not an assessment report.

A defensible report gives executive summary, written scope and permitted timeframe, method/versions, risk and limitations, evidence-backed findings, recommended remediation, retest status and owner-facing conclusions. Separate **observation** (e.g. packet returned SYN/ACK) from **inference** (likely reachable TCP service) and **confirmed vulnerability** (product/build and applicable flaw validated). A script failure is inconclusive; a port label or banner does not prove CVE applicability.

Finding example (fictional): `FINDING-01 | scope: approved lab device A | observation: test protocol exposes a generic product banner | risk: assists fingerprinting | verification: unconfirmed | recommendation: minimize unnecessary metadata and restrict access | retest: pending`. Do not present this example as an actual discovered issue.

Only publish original screenshots from the student's own authorized course environment after removing identities, IP addresses, hostnames, passwords, account names, paths, VM and HomeLab labels, and hidden metadata. Lecture slides, other people's demo captures and worksheet expected outputs are **not** proof of personal execution. Store original evidence privately if authorized and preserve timestamp, command, output, environment, troubleshooting and limits. No sanitized original lab screenshot was supplied for verification; none is added.