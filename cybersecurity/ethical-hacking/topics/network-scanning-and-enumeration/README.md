# Network Scanning And Enumeration

## What the practical worksheet teaches
The available Nmap scanning lab introduces a Kali Linux and deliberately vulnerable VM learning environment. Scanning is for assessing specifically authorized systems, not arbitrary Internet targets.

## Interpreting open, closed and filtered services
An **open** port suggests a service responded in a way consistent with accepting that type of connection. **Closed** generally means reachable but not listening. **Filtered** means a firewall or other issue prevents reliable determination. These are observations dependent on probe type and path.

## TCP scan interpretation
A SYN-based probe can identify how the target responds before a full application session. Alternative TCP flag approaches may elicit different responses depending on operating system and filtering. A TCP SYN does not prove the application accepted or processed a connection.

## Service and host identification
Version identification attempts to determine the product behind a responsive service. Operating-system fingerprinting infers platform behavior from multiple network characteristics, but results can be ambiguous. Port-based assumptions (e.g. port 80 always implies HTTP) must be confirmed.

## Timing, scope and scripts
Scan rates affect network load and quality of results. Script-based enumeration can identify configuration clues but requires manual interpretation; scanner findings can be incorrect or incomplete. A banner might disclose software but is not itself proof of exploitation.

## AI-assisted interpretation
The lab discusses using a local language model to interpret scan results. Language models can propose inaccurate conclusions or unsafe actions; manual verification and test authorization remain necessary.

## Actual achievement status
This is a detailed explanation of the lab worksheet; successful execution and full screenshots were not verified. Add each real lab output when completed and explain what it proves and does not prove.