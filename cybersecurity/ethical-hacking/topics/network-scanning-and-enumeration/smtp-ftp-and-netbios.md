# SMTP, FTP, SMB and NetBIOS: enumerating exposed service behavior

Service enumeration interacts with a listening protocol to learn more than a port scan alone. It can reveal banners, object names, account disclosure and permissive settings. Every request must remain within authorized assets, identities and volume.

## SMTP (Simple Mail Transfer Protocol)

SMTP transfers mail server-to-server on TCP/25, while submission commonly occurs on TCP/587 and implicit TLS submission on TCP/465. Plain TCP connectivity is insufficient to prove authentication or mail relay is permitted. A server can expose a banner and still limit actual operations.

Illustrative protocol conversation on a synthetic service:

```text
nc -nv <AUTHORIZED_MAIL_HOST> 25
HELO example.test
VRFY testuser
QUIT
```

`telnet <AUTHORIZED_MAIL_HOST> 25` is an alternate plain connection method. `220` is a service greeting, `250` typically indicates a positive completed action, `252` means the server cannot verify the user but will accept the message, and `550 5.1.1` commonly indicates unknown recipient. **252 does not confirm a valid account.** Server policy, catch-all forwarding, anti-enumeration behavior and different SMTP commands can change responses.

Additional tools covered include `smtp-user-enum`, Nmap's `smtp-enum-users`, and Metasploit `auxiliary/scanner/smtp/smtp_enum` with `RHOSTS`, `RPORT`, `USER_FILE`, `THREADS`, and `METHOD` (VRFY, EXPN or RCPT). Each method can produce log events and false positives. Bulk account guessing may violate the agreed testing scope and trigger throttling.

**Defense:** restrict VRFY and EXPN, normalize account-specific errors, monitor enumeration attempts, enforce authenticated submission and TLS, restrict exposed service interfaces and avoid unintended open relay.

## FTP (File Transfer Protocol)

FTP typically uses TCP/21 for the control connection; data connections depend on active/passive mode and firewall configuration. A banner can disclose product/version and an anonymous session may expose a directory listing. `ftp-anon` checks permissive access. The source also illustrates Metasploit `auxiliary/scanner/ftp/ftp_login` for credential checks, which must never be interpreted as harmless discovery when login attempts are involved.

A `230` response commonly signals successful authentication; `530` indicates failed or unavailable login; `150` means a file operation/data transfer is beginning. Being able to list a directory does not prove the ability to read, write or download arbitrary files. Default FTP transmits credentials and data without encryption, unless a protected variant is configured.

**Defense:** disable unnecessary anonymous access, enforce least privilege, restrict writable directories, monitor login attempts and prefer SSH File Transfer Protocol (SFTP) or properly secured FTPS when appropriate.

## NetBIOS and SMB

NetBIOS names identify Windows networking resources within older naming/session mechanisms. UDP/137 supports NetBIOS name service, TCP/139 NetBIOS session transport, and TCP/445 direct SMB. A name returned by `nbtscan <AUTHORIZED_HOST>` is host-identification evidence, not proof that SMB sharing is enabled. SMB shares require authorization and can have different read/write permissions even when names are visible.

The source introduces `enum4linux`, NetBIOS tooling and SMB enumeration. Findings might include machine names, workgroups, shares and user/group metadata. Check guest/anonymous access and share permissions only within approved test identities. Restrict access to 137/139/445, disable unnecessary NetBIOS, avoid public SMB exposure, enforce SMB signing and permissions appropriate to policy, and monitor access logs.

## Other service enumeration

DNS may expose names and records; an AXFR zone transfer over TCP/53 is generally authorized only between configured DNS peers. NTP reveals time synchronization behavior but not an authenticated asset inventory. Telnet sends unencrypted application data and should not be exposed for sensitive administration. These are distinct services with different permissions and visibility. Network-monitoring suites and packet analyzers can corroborate protocol behavior but cannot replace application authorization or verified findings.

## Interpreting and troubleshooting

An open TCP port is not proof the corresponding service is actually reachable through a meaningful protocol. Timeouts can be firewall or routing behavior. SMTP acceptance is not automatic proof of account existence; SMB share disclosure is not proof of readable sensitive contents; FTP login success is not permission to retrieve files. Document the exact synthetic protocol interaction, response codes, scope and uncertainty rather than claiming broad compromise.