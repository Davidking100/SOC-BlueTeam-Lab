# SOC Lab 06: Microsoft Sentinel Brute Force Detection

## Objective
Build and deploy a detection rule in Microsoft Sentinel to identify RDP brute force attacks using KQL.

## Tools Used
- Microsoft Sentinel SIEM
- Kusto Query Language (KQL)
- Azure SecurityEvent Logs

## Detection Details

### Analytics Rule
**Name**: Brute Force Detection - RDP  
**MITRE ATT&CK**: T1110 - Brute Force  
**Severity**: Medium  
**Logic**: Triggers when >= 5 failed logins (EventID 4625) occur within 5 minutes

### KQL Query
```kql
SecurityEvent
| where EventID == 4625 
| summarize FailedCount = count() by TargetAccount, Computer, bin(TimeGenerated, 5m)
| where FailedCount >= 5

