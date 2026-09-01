
Big Billion <davidogun100@gmail.com>
10:42 PM (0 minutes ago)
to savenet419

# SOC-BlueTeam-Lab 🛡️
Documenting my journey to becoming a Tier 1 SOC Analyst through hands-on labs, alert triage, and detection engineering.

## About Me
Aspiring SOC Analyst currently training with Let'sDefend SOC Simulator. 
Focus: SIEM, Incident Response, Threat Detection, MITRE ATT&CK

## 📁 Repository Structure
## 🚀 Day 1 Progress - 3 Alerts Closed
| Alert ID | Type | Verdict | MITRE ATT&CK |
| --- | --- | --- | --- |
| SOC282 | Phishing Email | True Positive | T1566.001 |
| SOC153 | Suspicious Powershell | True Positive | T1059.001 |
| SOC127 | SQL Injection | True Positive | T1190 |

All case studies and screenshots are in `01-SIEM-Alerts/`

## 🛠️ Tools in My Home Lab
- Splunk Free - SIEM
- Wazuh - EDR/SIEM
- Sysmon - Windows Logging
- Atomic Red Team - Attack Simulation

## Goals
Complete 7-day SOC Bootcamp and document 15+ alerts with full IR workflow.

## Connect
LinkedIn: 


## Week 2: SIEM Skills
- Built Splunk Playbook with 3 triage queries for SOC Analyst role




## Case 01: Brute Force Attack Detection

**Scenario**  
An attacker attempted to brute force user accounts by sending multiple failed login requests from a single IP address.

**Alert Details**
- **Severity**: High
- **Source**: Web Server Logs
- **Indicator**: 127 failed login attempts from `192.168.1.10`

**Detection**
- **Tool Used**: Splunk Enterprise
- **SPL Query**: [`brute-force-splunk.spl`](/03-SIEM-Queries/brute-force-splunk.spl)

**Investigation & Findings**
Ran SPL query to count failed 401s by source IP. Result:  

**Result**: `192.168.1.10` had 4 failed login attempts within 5 seconds. This exceeded our threshold of 3 attempts.

**Evidence**
![Splunk Brute Force Detection](02-Evidence/screenshots/splunk-brute-force-detection.png)
*Figure 1: Splunk statistics showing 4 failed attempts from attacker IP*

**Containment & Response**
1. Blocked IP `192.168.1.10` at firewall
2. Forced password reset for targeted accounts  
3. Created alert rule for future brute force attempts
4. Notified SOC Lead

**MITRE ATT&CK**: T1110.001 - Brute Force: Password Guessing



## Case 02: Suspicious PowerShell Detection

**Scenario**  
An endpoint executed a suspicious PowerShell command with encoded parameters, likely used to download and execute malware without touching disk.

**Alert Details**
- **Severity**: Critical
- **Source**: Windows Event Logs 4104 + Sysmon
- **Indicator**: `powershell.exe -encodedcommand JABzAD...`

**Detection**
- **Tool Used**: Splunk Enterprise + Sysmon
- **SPL Query**: [`suspicious-powershell.spl`](/03-SIEM-Queries/suspicious-powershell.spl)

**Investigation & Findings**
Searched for ProcessName=powershell with encoded flags. Result:  
`WKSTN-042` User `jdoe` executed encoded PowerShell that called `Invoke-WebRequest` to `http://malicious.com/payload.exe`.

**Evidence**
*Screenshot: Splunk detection showing 1 event - Computer: WKSTN-042, User: jdoe, Flags: -encodedcommand, CommandLine: powershell.exe -e JABzAD0ATgBl...*
*Image pending upload*

**Containment & Response**
1. Killed malicious `powershell.exe` process on `WKSTN-042`
2. Isolated host from network via EDR
3. Blocked C2 domain `malicious.com` at firewall
4. Searched for persistence in Task Scheduler and Registry Run keys

**MITRE ATT&CK**: T1059.001 - Command and Scripting Interpreter: PowerShell


# SOC Blue Team Lab
**By Davidking100**

Hands-on SOC analyst portfolio with 5 incident response case studies.

## 📁 Case Studies
- **[Case 01: Brute Force Attack](./03-SIEM-Queries/Case-01-BruteForce.md)** - SIEM Alert Thresholds
- **[Case 02: Suspicious DNS Tunneling](./03-SIEM-Queries/Case-02-Suspicious-DNS.md)** - Network Anomalies  
- **[Case 03: DNS Traffic Baseline](./03-SIEM-Queries/Case-03-DNS-Traffic-Baseline.md)** - Threat Hunting
- **[Case 04: Suspicious PowerShell](./03-SIEM-Queries/Case-04-Suspicious-PowerShell.md)** - LOLBAS + EventID 4104 + MITRE
- **[Case 05: Phishing Email Triage](./04-Phishing-Analysis/README.md)** - IOC Extraction + MITRE
- **[Case 06: Malware Alert Investigation](./05-Malware-Alert-Investigation/README.md)** - EDR + Process Analysis

## 🛠️ Tools Used
Splunk/SIEM, Wireshark, VirusTotal, Microsoft Defender, MITRE ATT&CK

## 🎯 Goal
Demonstrate practical blue team skills for SOC Analyst Level 1 roles.

# SOC L1 Portfolio - David Oluwatosin

Aspiring SOC L1 Analyst | Microsoft Defender XDR | Azure Sentinel | KQL | Incident Response

This repository documents my hands-on incident response labs. Each lab follows a full IR workflow: Detect > Investigate > Contain > Document.

## Labs

| Lab # | Title | Attack Type | Tools Used | Status |
| --- | --- | --- | --- | --- |
| 08 | Data Exfiltration Investigation | Insider Threat / Exfiltration | Defender XDR, KQL | [View Report](./Incidents/LAB08-DataExfiltration.md) |
| 09 | Phishing Investigation | Initial Access / Phishing | Defender XDR, EmailUrlInfo KQL | [View Report](./Incidents/LAB09-Phishing.md) |
| 10 | Malware Infection Investigation | Execution / C2 | Defender XDR, Process KQL | [View Report](./Incidents/LAB10-Malware.md) |

## Technical Skills
**SIEM & EDR:** Microsoft Defender XDR, Azure Sentinel, Splunk, Elastic  
**KQL:** EmailEvents, EmailUrlInfo, DeviceNetworkEvents, DeviceProcessEvents, DeviceFileEvents  
**IR:** Alert Triage, Incident Classification, Containment, Forensics, Reporting  
**Framework:** MITRE ATT&CK

## About Me
Security Operations Analyst based in Lagos, Nigeria. Open to remote 24/7 MSSP SOC roles.
Connect with me on LinkedIn: https://www.linkedin.com/in/david-oluwatosin-233917158/

