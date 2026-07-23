# SOC127 - Web Application Attack Blocked

**Date**: 2026-04-27  
**Platform**: Let'sDefend SOC Simulator  
**Severity**: High  
**Verdict**: True Positive ✅

## 1. Alert Summary
WAF blocked SQL Injection attack attempt targeting login form.

## 2. IOCs
| Type | Value |
| --- | --- |
| Source IP | `185.12.45.99` |
| Target URL | `/login.php` |
| Payload | `' OR 1=1--` |

## 3. Actions Taken
1. Blocked source IP in firewall
2. Confirmed WAF rule triggered correctly
3. Checked logs for successful logins - none found

## 4. MITRE ATT&CK
**T1190 - Exploit Public-Facing Application**
