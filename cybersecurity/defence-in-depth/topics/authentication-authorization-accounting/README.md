# Authentication, Authorization and Accounting (AAA)

**Evidence:** lecture and study-material explanation. The CLI is illustrative; no authenticated session, accounting record or server trace is independently verified.

## Three independent questions

**Authentication — who are you?** A router, access device or network application checks claimed identity against a local database or external service. **Authorization — what may you do?** Policy determines permitted EXEC sessions, commands and network resources. **Accounting — what happened?** Records establish session times, command/activity or resource usage for auditing and troubleshooting. A successful authentication can coexist with failed authorization. The lecture categorizes accounting as network, connection, EXEC, system, command and resource events.

The configuration flow in the diagrams is: administrator connects to router (the AAA client / network access device) → router solicits credentials → local user database or central AAA service evaluates them → authorization supplies permitted actions → accounting records the resulting activity. In **local AAA**, configuration and identity records live on each router. **Server-based AAA** centralizes consistent access policy and reporting but introduces dependency on reachability, time, keys and server health. The lecture uses Cisco ACS, Active Directory integration and ISE as architectural references; these do not prove a deployed service.

## RADIUS and TACACS+ at protocol level

| Attribute | RADIUS | TACACS+ |
| --- | --- | --- |
| Transport | UDP 1812 authentication/authorization and 1813 accounting | TCP 49 |
| Policy model in course | Authentication and authorization typically combined | Separate authentication, authorization and accounting exchanges |
| Packet protection as taught | Shared-secret mechanism obscures the password field; packet is not fully encrypted | Packet body is encrypted, header remains visible |
| Common fit | Network access, 802.1X and subscriber authentication | Granular network-device administration and command authorization |

Neither protocol should be described as “encrypting the entire packet including header.” Shared secrets must match and must **never** be included in public configuration examples. Server availability fallback must be designed carefully: many IOS AAA method lists try the next method on an **error/unavailable** result, not on an explicit **reject**.

## Method lists and local fallback

```cisco
! Conceptual IOS method-list pattern; no live credentials shown.
aaa new-model
aaa authentication login default group tacacs+ local
aaa authentication login REMOTE group radius local
line vty 0 4
 login authentication REMOTE
 transport input ssh
```

`aaa new-model` enables AAA processing. `default` is a system-defined method list; `REMOTE` is a named list applied to VTY. The first method represents a server group; `local` is a deliberate fallback **when the server is unreachable**. Local usernames/secrets must be provisioned through secure administration, omitted here. Changing AAA on the only remote session risks lockout: preserve console/OOB access, test a second session, check method-list binding and have a rollback plan. The practice questions also contrast `local` and `enable` fallbacks; they have materially different security properties.

A typical external-server design must specify server address, protocol/port, source interface and a matching secret **privately**, then apply explicit authentication and, if necessary, EXEC/command authorization and accounting lists. `tacacs-server ... single-connection` in a legacy example maintains a TCP session for efficiency; it is not a substitute for authorization. Prefer platform-supported named server objects rather than blindly copying legacy syntax.

## Authorization, accounting and 802.1X

AAA authorization may gate `exec` launch or specific privilege-15 commands; `aaa authorization exec` and `aaa authorization commands` govern different scopes. A custom list must be applied to the intended line/context. Accounting modes such as `start-stop` record lifecycle events, subject to configured backend and policy. Do not equate merely enabling an accounting command with receiving records at a collector.

For **802.1X**, the **supplicant** is the endpoint, the **authenticator** is typically a switch or WLAN access point and the **authentication server** is commonly RADIUS-backed. EAP messages are relayed through the access device before controlled-port access is granted. A diagram would show endpoint ↔ switch/AP ↔ RADIUS service, with the switch enforcing the result; endpoint authorization is distinct from logging in to the router itself.

## Troubleshooting decision tree

1. Confirm management-plane connectivity and time between network access device and server without printing shared secrets.
2. Check correct TACACS+/RADIUS protocol, destination port, server object, source interface and authorized NAS client.
3. Confirm `aaa new-model`, method-list **names/order**, and which list is applied to console/VTY/EXEC.
4. Distinguish server **timeout**, explicit credential rejection and authorization rejection.
5. Correlate redacted device `debug aaa authentication` / `debug aaa authorization` or protocol-specific diagnostics with server logs, then disable verbose debug.
6. Verify both authorized login and denial, fallback during controlled server unreachability, restricted commands and actual accounting records.

**What I learned:** authentication success is not authorization success; fallback order and error semantics determine both security and recoverability. **Not verified:** server reachability, user session, explicit denial, fallback and records. See [practical exercise register](../../PRACTICAL_EVIDENCE.md).
