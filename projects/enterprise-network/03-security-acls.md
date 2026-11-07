# Switch Security, Remote Management and Access Control

## Port security
Selected switch access ports are documented with a maximum of **2** secure MAC addresses and violation action **restrict**. The `show port-security` output includes address/violation counts. One earlier screenshot reports a port as `secure-down`; an configured feature is not automatically an operational forwarding interface.

## DHCP snooping
DHCP snooping protects clients against untrusted DHCP responses by designating legitimate DHCP server/uplink interfaces as trusted. The report includes both an early screenshot where snooping appears **disabled** and later screenshots reporting **enabled** on selected VLANs. These represent different project states, not contradictory proof of one final moment.

## SSH-only access
IT workstations can manage network devices via SSH, while other users should be denied management access. The report shows a named standard ACL `IT-SSH-ONLY` applied using VTY `access-class` alongside `login local` and `transport input ssh`. An IT login succeeds in the demonstration and a Finance-side SSH attempt closes.

## Traffic policies
Named ACLs were used to: permit matching departments across sites, restrict unrelated cross-department connections, block ICMP to selected server addresses while allowing required application traffic, exclude HR and Finance from internet-edge translation, and permit only HTTP/HTTPS/SMTP for public-facing web and email servers.

**How to verify:** check ACL order/direction and traffic test results; a timed-out ping alone may indicate routing or host failure, not necessarily the intended ACL. Sources: pages 9–10, 18–23, 28–31, 44–47.