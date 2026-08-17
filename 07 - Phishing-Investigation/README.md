# Lab 07: Phishing Investigation & Detection Engineering
**SOC Analyst Portfolio Project**

## 1. Objective
Investigate potential phishing activity and engineer a custom detection rule in Microsoft Sentinel to monitor Microsoft Defender for Office 365 telemetry.

## 2. Environment
- **SIEM**: Microsoft Sentinel
- **Data Source**: Microsoft Defender for Office 365 Connector
- **Skill Focus**: Threat Hunting, KQL, Detection Engineering, Troubleshooting

## 3. Investigation Process

### 3.1 Initial Data Exploration
Ran proactive hunt queries against email telemetry to identify phishing indicators.
```kql
SecurityAlert
| where TimeGenerated > ago(7d)
| where ProductName == "Microsoft Defender for Office 365"
| where AlertName has "phish"


