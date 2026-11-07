# NAT, PAT, Internet Publishing and Wireless

## NAT and PAT
The project configures **PAT overload** for outbound users at each simulated ISP edge and static service mappings for selected servers. NAT changes address/port representation; it is not a full replacement for a firewall access-control policy.

| Site | Internal Web | External Web | Internal Mail | External Mail |
| --- | --- | --- | --- | --- |
| Bahrain | `10.10.90.10` | `200.10.10.10` | `10.10.90.11` | `200.10.10.11` |
| KSA | `172.16.90.10` | `200.20.20.10` | `172.16.90.11` | `200.20.20.11` |
| Oman | `192.168.90.10` | `200.30.30.10` | `192.168.90.11` | `200.30.30.11` |
| Qatar | `172.20.90.10` | `200.40.40.10` | `172.20.90.11` | `200.40.40.11` |

Web services use TCP 80/443, email SMTP uses TCP 25 in the report. The listed public IPs are simulation values, not evidence of address ownership.

## Wireless segmentation
Each site assigns Wi-Fi to **VLAN 100**, using `10.10.100.0/24`, `172.16.100.0/24`, `192.168.100.0/24` and `172.20.100.0/24` respectively. SSIDs are separated and wireless security is documented, but original passphrases are intentionally not published.

## Verification
`show ip nat translations` and `show ip nat statistics` describe translation state/counters. Test actual traffic from permitted and restricted users to verify intended behavior. Sources: pages 14, 17–18, 32–34, 40–44.