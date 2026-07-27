## Case 01: Brute Force Attack
**Alert**: 127 failed logins to admin@company.com from 185.220.101.33

**Query Used**:
index=security src_ip=185.220.101.33 user=admin@company.com EventCode=4625
| stats count

**Findings**: Confirmed brute force. 0 successful logins.

**Action**: Blocked IP at firewall. Forced password reset for admin.
