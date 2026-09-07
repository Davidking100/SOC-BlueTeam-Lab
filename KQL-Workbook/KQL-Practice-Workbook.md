# KQL Practice Workbook 🛡️
SOC L1 Analyst | Microsoft Defender XDR | Azure Sentinel

This workbook contains all KQL queries used in my SOC labs. 
Purpose: Daily practice for Alert Triage, Threat Hunting, and Incident Response.

Run these in: Microsoft 365 Defender > Hunting > Advanced hunting or Azure Sentinel > Logs

---

## LAB 01: SIEM Alerts Triage
Goal: Daily SOC dashboard and alert prioritization

```kql
// Query 1.1: Top 10 Alerts Last 24 Hours
AlertInfo
| where TimeGenerated > ago(24h)
| summarize Count=count() by Title, Severity, ServiceSource
| top 10 by Count desc

// Query 1.2: High Severity Unresolved Alerts

AlertInfo
| where Severity == "High" and Status in ("New", "InProgress")
| project TimeGenerated, Title, Severity, ServiceSource, AlertId
| order by TimeGenerated desc

