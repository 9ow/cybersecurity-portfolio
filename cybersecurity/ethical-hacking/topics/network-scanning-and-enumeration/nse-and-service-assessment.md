# Nmap Scripting Engine: service discovery and vulnerability checks

The Nmap Scripting Engine executes Lua scripts in association with discovered hosts/services. Script output can reveal configuration evidence or signs of a known issue, but must be interpreted with the script implementation, version, response and false-positive risk in mind.

## Syntax

```bash
nmap --script-help http-title
nmap -sV -p 80,443 --script http-title <AUTHORIZED_HOST>
nmap -sV -p 21 --script ftp-anon <AUTHORIZED_HOST>
nmap -sV -p 445 --script smb-enum-shares <AUTHORIZED_HOST>
nmap --script-updatedb
```

`--script-help` describes script assumptions and arguments. `--script name1,name2` selects multiple named scripts; `--script-args key=value` provides script-specific configuration; `--script category` selects a class, often broader than anticipated. Script directories commonly include `/usr/share/nmap/scripts/`.

## Script categories

- `default`: standard bundled selection executed by `-sC`.
- `safe`: intended lower-risk scripts; still validate volume and side effects.
- `discovery`: collects system/service information.
- `version`: improves product detection.
- `auth`: checks authentication mechanisms and sometimes access-control behavior.
- `broadcast`: discovers devices using local broadcast behavior.
- `external`: communicates with third-party services; consider privacy.
- `vuln`: checks likely vulnerable conditions.
- `brute`: performs repeated credentials attempts; can cause lockouts.
- `intrusive`, `dos`, `exploit`, `fuzzer`: potentially disruptive or exploitative and require explicit authorization.
- `malware`: identifies malware-related indicators.

## What named scripts do

| Script | Question it answers | What it cannot establish by itself |
|---|---|---|
| `http-title` | What title an HTTP endpoint returns | Application identity, patch state or a vulnerability |
| `http-enum` | Which common URL paths respond | Authorization to retrieve contents; paths may be false positives |
| `ftp-anon` | Whether an FTP server accepts anonymous authentication | Access to every directory or the sensitivity of stored data |
| `smb-enum-shares` | Which SMB shares are disclosed to the current session | Effective write permissions for every principal |
| `smb-vuln-ms17-010` | Whether an SMB behavior resembles a known issue | An exploit has succeeded, or every patch is absent |
| `ssl-heartbleed` | Whether TLS behavior matches CVE-2014-0160 indicators | Exposure of actual secret data or affected business impact |
| `dns-brute` | Which candidate subdomain labels resolve | A complete domain asset inventory |
| `ssh-hostkey` | Public host-key algorithm and fingerprint | Trustworthiness of the host or password strength |
| `ssl-enum-ciphers` | Negotiated TLS version/cipher support | Full application security |
| `smtp-enum-users` | Whether server responses discriminate usernames | Definitive account existence with catch-all responses |

The material also describes `ftp-brute` and `ssh-brute` as credential-guessing mechanisms; they are not routine discovery. Limit to explicitly approved synthetic identities if ever used. A script expression such as `--script 'http*'` selects all matching scripts, **not** necessarily safe HTTP-only checks. `--script vuln` and `--script 'auth,default,vuln'` can cause a wider investigation than a single check.

## Interpreting a result

An NSE section is normally nested beneath a `PORT STATE SERVICE` row or host summary. Distinguish:
- **Observed response:** e.g., an HTTP title was returned or SMB provided a share name.
- **Heuristic indicator:** a script compares response patterns and labels suspected vulnerability.
- **Confirmed finding:** independently validated affected configuration/build and supported by an applicable advisory and non-destructive evidence.
- **Inconclusive:** script error, timeout, missing authentication, a firewall rejection or ambiguous handshake.

No result is not proof of secure configuration. Large `vuln` sets may produce script failures that require separate triage. Validate tool version and underlying NSE script definitions rather than trusting category labels.

## Defensive and reporting value

Results inform inventory cleanup, exposed-service reduction, anonymous access review, SMB hardening and TLS modernization. Record exact script names, versions, settings, intended probes and sanitized outputs. Never reproduce credentials, actual private targets, share contents or directory data in a public portfolio.