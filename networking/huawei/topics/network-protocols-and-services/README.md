# Network Protocols And Services

**Source:** `Network Basics and Application layer services(1).pptx` (25 slides). **Study recorded; lab not verified.**

## Slides 4–9 — models/protocols
- Applications generate data (text, pictures, numbers, sound, video); engineers consider end-to-end transmission.
- **OSI**: proposed by ISO 1984, **7 layers**: Application interfaces to programs; Presentation format translation; Session establish/manage/end sessions; Transport end-to-end transmission/order/speed; Network logical addresses and delivery; Data Link frames/error detection; Physical bitstreams and electrical/physical characteristics.
- **TCP/IP standard** has **4 layers**: Application, Host-to-host, Internet, Network interface. Slide 6 separately shows a 5-layer *equivalent* depiction; do not conflate.
- Protocol placement from slide 7: application **Telnet FTP TFTP SNMP HTTP SMTP DNS DHCP**; transport **TCP UDP**; network **ICMP IGMP IP**; data link **PPPoE Ethernet PPP**.

## Slides 10–16 — application services
- **FTP** transfers upload/download using C/S architecture and two connections. Control client→server TCP **21** in both modes. Active (slide calls *proactive*, its stated default): server port **20** initiates data to client temporary port. Passive: client initiates data to server temporary port.
- **SFTP** based on SSH, one encrypted channel (auth and file contents), default port **22**; FTP plaintext dual-channel.
- **Telnet** remote client commands execute on server as if at console; plaintext. **STelnet** secured by SSH on port **22**, with stages: version → algorithm → key exchange → user authentication → session interaction.
- **HTTP** publish/receive HTML pages. **HTTPS** adds TLS: authentication, encryption, integrity; default ports HTTP **80**, HTTPS **443**.
- **DNS** maps domain name to IP; static resolution first, dynamic if static fails.

## Slides 17–25 — devices
- Campus: access / aggregation / core / egress layers, switches, routers, firewall, servers.
- Switch forwards local frames using **MAC-to-port table** at data-link layer; router moves IP packets between networks at network layer; firewall controls/security-filters at borders.
- Firewall history: packet filtering → application proxy → stateful inspection → UTM → NGFW; diagram/timeline details in PPT.
- Lecture ends with a multiple-answer application-layer protocol review.

## Recorded weaknesses
Full mock **14/15** (passive FTP missed), later diagnostic **14/15** (active FTP missed, 50% confidence). Correct but uncertain: TCP/IP model **75%**, Telnet **50%**, HTTPS **75%**. No verified lab results.
