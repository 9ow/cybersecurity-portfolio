# Wireshark — Network Traffic Analysis


## Skills applied

### Reading packet captures
- Opened existing PCAP files for offline inspection and used Wireshark's packet list, packet details and byte views to inspect captured traffic.
- Distinguished an offline PCAP from a live interface capture: opening a file analyzes saved packets; selecting an interface such as `ens224` observes new traffic on that interface.
- Used protocol, source/destination, port and packet information as starting points for analysis.

### Display filters
- Used Wireshark display filters, including `http`, to narrow the visible packet list without changing the underlying capture.
- Learned to check filter syntax and verify that a filter matches the intended traffic before interpreting an empty result.
- Compared the filtered view with the overall packet count to avoid confusing displayed packets with total captured packets.

### HTTP analysis and exported objects
- Inspected HTTP traffic in `Wireshark-lab-2.pcap` and used **File → Export Objects → HTTP** to identify files transferred in captured HTTP responses.
- Identified the image `Rise-Up.jpg` among exported HTTP objects and inspected the extracted image.
- Learned that application-layer objects can sometimes be reconstructed from captured traffic, depending on the protocol and capture completeness. This does not imply that encrypted HTTPS payloads are readable without decryption.

### TCP conversations and stream inspection
- Used Wireshark's conversation statistics to identify communicating endpoints and narrow the analysis to a TCP exchange.
- Practiced the workflow of following a TCP stream to inspect the sequence of application data, rather than treating individual packets in isolation.
- Understood that a TCP connection or a visible port alone does not prove successful exploitation or compromise.

### Guided capture review
- Opened `guided-analysis.pcap` and inspected its TCP conversation and packet statistics.
- Confirmed the capture contained **44 packets**.
- Completed the associated guided-analysis questions.


## Repeatable analysis workflow
1. Open the PCAP and confirm the capture context and packet count.
2. Review endpoints, protocols and conversations before filtering.
3. Apply a focused display filter and inspect matching packet details.
4. Follow relevant TCP streams when application content is available.
5. For HTTP object transfers, use **Export Objects → HTTP** and inspect recovered files.
6. Separate direct observations from hypotheses and record the relevant packet numbers when investigating.

## Key distinctions
| Concept | Practical meaning |
| --- | --- |
| Capture filter | Limits traffic collected during capture |
| Display filter | Changes what Wireshark shows from an existing capture |
| TCP conversation | A pair of communicating endpoints/ports, not evidence of compromise by itself |
| Follow TCP Stream | Reassembles and displays available stream data for interpretation |
| Export HTTP Objects | Extracts reconstructable objects from HTTP traffic in a capture |
| Offline PCAP vs live capture | Saved evidence versus newly observed interface traffic |
