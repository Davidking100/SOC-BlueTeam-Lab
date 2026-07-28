## Case 02: DNS Tunneling / Data Exfiltration
**Date**: 2026-07-28
**Analyst**: Big Billion
**Severity**: Critical

**Alert**: EDR detected 4,238 DNS queries in 2 minutes to x9k2p4m8.data-exfil.net 
from host 192.168.1.105

**Investigation**:
- Tool: Wireshark
- Filter: dns
- Findings: Confirmed abnormal DNS traffic. Source making high volume of random 
  subdomain queries. Pattern consistent with DNS tunneling for data exfiltration.

**Actions Taken**:
1. Isolated endpoint 192.168.1.105 from network
2. Blocked *.data-exfil.net at firewall 
3. Escalated to Incident Response team - Ticket #INC002

**Status**: Contained. Awaiting IR follow-up.
