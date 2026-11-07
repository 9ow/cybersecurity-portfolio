# Professional security assessment reporting

## Evidence to conclusion

Security documentation should be reproducible, scoped, concise enough to review and detailed enough to defend technically. Differentiate a **fact** (the tool received a response), an **inference** (the response is consistent with a service or configuration), a **suspected weakness** (likely issue) and a **confirmed finding** (validated applicability and material effect). Avoid using an isolated banner, port scan or AI summary as proof of compromise.

## Recommended deliverable structure

- **Executive context:** objectives, authorization and high-level exposure with audience-appropriate language.
- **Scope and constraints:** systems included and excluded, assessment period, permissions, prohibited operations and unavailable testing access.
- **Methodology:** passive research, discovery, fingerprinting, service-specific enumeration and relevant verification steps.
- **Findings:** sanitized unique reference, description, affected component class, evidence, severity rationale, likelihood/impact considerations, compensating controls, remediation owner/action and retest criteria.
- **Limitations:** scan filtering, skipped methods, uncertain service versions, incomplete directory privileges, omitted network segments and tools that timed out.
- **Remediation prioritization:** emergency exposures vs planned patching, architectural controls and visibility improvements.

## Fictional illustrative finding

`F-EXAMPLE-01` — **Excessive metadata exposure on a management service**. Observation: the service returns descriptive version and interface fields to a configured read-only management identity. Impact: improves an attacker's targeting if the management interface is reachable and credentials are compromised. Validation: review allowed MIB views, network ACL and authentication mode. Mitigation: restrict management subnet, migrate to authenticated encrypted SNMP and limit returned MIB objects. Status: demonstration only; no actual affected asset or completed retest.

## Quality and privacy controls

Do not include actual target identifiers, passwords, private domain names, personally identifying records, infrastructure drawings or original raw scan output in a public repository. Replace targets with uppercase placeholders and use reserved example domains. If original screenshots are ever provided, review visible terminal prompt, navigation bar, clocks, paths, hostnames, interface addresses and embedded metadata before publication. Current materials establish technical study, not independent proof that a particular command ran successfully in a personally controlled environment.

## Troubleshooting narrative

For every issue document expected behavior, what was observed, alternate explanations, authorized non-destructive follow-up and unresolved questions. For instance, `open|filtered` on UDP is an uncertainty; it is **not** equivalent to `open`. A directory query with `result: 0 Success` but zero entries may be correct access control, filter mismatch or missing objects. Reporting should preserve this distinction.