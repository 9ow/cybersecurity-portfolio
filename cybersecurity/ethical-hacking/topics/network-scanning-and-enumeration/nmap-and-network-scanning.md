# Network scanning and Nmap

Source: Unit 3 slides 3–41. Commands below are sanitized slide examples, not personally executed scans. `<LAB_HOST>` and `<LAB_CIDR>` mean a separately authorized course target.

## TCP/UDP behavior

TCP connects through SYN → SYN/ACK → ACK. SYN opens, ACK acknowledges, FIN closes orderly, RST resets, PSH requests prompt delivery, URG marks urgent data. NULL scanning means *no flags*, not a NULL flag. `-sT` completes a TCP handshake; `-sS` probes SYN and typically resets before completion. A SYN/ACK suggests open; RST suggests closed; no reply or particular ICMP errors may suggest filtered. A SYN scan is not invisible to IDS.

`-sF` FIN, `-sN` NULL and `-sX` Xmas (FIN/PSH/URG) produce RST for closed TCP ports on conforming implementations; no answer means **open|filtered**, not proven open. They are unreliable on some Windows stacks. `-sA` tests *filtered/unfiltered*, not open versus closed. `-sU` queries UDP; a UDP response indicates open, ICMP port unreachable indicates closed, silence is often **open|filtered**. UDP lack of reply is not reliable proof of open status.

## Common options

`nmap <LAB_HOST>` one authorized host; `nmap <LAB_CIDR>` a range only if every address is scoped; `-iL hosts.txt` reads approved targets; `-p 80`, `-p 20-23`, `-p 80,443`, `-p-` select one, range, list or all TCP ports; `-sS -sU -p U:53,T:22` selects mixed transport ports. CIDR `/24` should not be called a class-C address by assumption.

`-sn` discovers responsive hosts without port scans (older lecture uses `-sP`); `-PE` uses ICMP echo discovery; `-PS22,80` sends TCP SYN discovery probes, and `-Pn` skips discovery and attempts scan as though the host is online—it does **not** disable port scanning. `-sV` probes service versions; `-O` estimates OS by fingerprint; `-A` enables OS/version/default-script/traceroute functionality; `-sC` runs default scripts. Guessed banners, service labels and OS fingerprints require corroboration, especially behind proxies or NAT.

`-T0` through `-T5` select increasing timing aggressiveness; low speed does not promise IDS evasion and high speed can miss results. `--max-rate` limits sending rate; `--max-parallelism` caps simultaneous probes. `-v` increases verbosity; `-V` shows Nmap version. `--open` filters output display. `-oN`, `-oG`, `-oX`, `-oA` save normal, legacy grepable, XML or all three formats. Preserve raw evidence privately and redact public copies.

## NSE scripts

Lua-based Nmap Scripting Engine supports `--script <name>`, `--script-help <name>`, `--script-args`, `--script-updatedb`; Linux installs commonly use `/usr/share/nmap/scripts/`. The slide categories are auth, broadcast, brute, default, discovery, dos, exploit, external, fuzzer, intrusive, malware, safe, version and vuln. Category membership is not proof that a script is harmless.

`http-title` retrieves page title; `http-enum` tests common paths; `ftp-anon` checks anonymous FTP access; `smb-enum-shares` lists disclosed SMB shares; `smb-vuln-ms17-010` tests signs of a particular SMB weakness; `ssl-heartbleed` checks historical OpenSSL exposure; `dns-brute` probes subdomain candidates. `ftp-brute` and `ssh-brute` can trigger account lockouts; do **not** use without specific written permission. Broad wildcards such as `--script="http*"` or category `vuln` can include intrusive checks and must be reviewed individually. A `VULNERABLE` script result needs independent validation; a script error is inconclusive.

The lecture also covers IPv6 (`-6`), limited proxy support (`--proxies`), and source-IP choice (`-S`) whose results and permission constraints vary. AI scanning discussion includes local Ollama for draft command generation and interpretation; no installation or execution is verified, and model suggestions must be checked against scope. Lecture screenshot commands/results are instructor examples and are not republished as personal work.

For source guidance: https://nmap.org/book/man.html.