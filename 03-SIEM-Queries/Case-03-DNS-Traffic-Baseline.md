## Case 03: HTTPS/TLS Traffic Baseline
**Date**: 2026-07-28
**Analyst**: Big Billion
**Tool**: Wireshark
**Filter**: tls

**Findings**:
Captured TLSv1.2 and TLSv1.3 traffic. Observed legitimate connections to:
- eu-teams.events.data.microsoft.com (SNI field)
- github.com (140.82.114.25)

**Analysis**: No anomalies detected. Traffic volume and destinations match 
expected business activity. SNI fields show legitimate Microsoft and GitHub domains.

**Conclusion**: Baseline traffic is clean. No C2 or data exfil detected.
