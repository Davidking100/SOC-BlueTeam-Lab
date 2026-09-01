# LAB 08: Suspicious Data Exfiltration Investigation

## 1. Incident Details
**Incident ID:** INC-2026-08-008
**Date/Time Detected:** 2026-08-18 14:22:00 UTC
**Date/Time Contained:** 2026-08-18 14:35:00 UTC
**Classification:** True Positive
**Severity:** High
**Analyst:** David Oluwatosin
**Status:** Closed
**Data Sources:** Microsoft Defender XDR - DeviceNetworkEvents, DeviceFileEvents

## 2. Summary
Detected a workstation uploading a large.zip file to an unauthorized external cloud storage domain. This indicated potential data exfiltration by an internal user.

## 3. Timeline - 5 W's
- **What:** Large outbound file upload to external domain
- **When:** 2026-08-18 14:22:00 UTC
- **Where:** Device: `LAPTOP-42`, User: `jdoe@contoso.com`
- **Who:** Internal User: `jdoe@contoso.com`
- **How:** Uploaded `HR_Records.zip` to `dropbox.com` via Chrome. ~2.3GB transferred

## 4. Investigation Steps
kql
// Step 1: Find suspicious outbound traffic

DeviceNetworkEvents
| where TimeGenerated > ago(7d)
| where RemoteUrl contains "dropbox.com"
| where ActionType == "ConnectionSuccess"
| summarize TotalBytesSent = sum(SentBytes) by DeviceName, RemoteUrl

// Step 2: Correlate with file activity

DeviceFileEvents
| where DeviceName == "LAPTOP-42"
| where FileName endswith ".zip"
| project TimeGenerated, FileName, FolderPath, SHA1```


Findings:
    1. Device LAPTOP-42 sent 2.3GB to dropbox.com
    2. File C:\Users\jdoe\Documents\HR_Records.zip created 5 min before upload
    3. User jdoe@contoso.com is not in HR/IT and not approved for external sharing 

## 5 Containment & Remediation Actions 
-  Isolated device LAPTOP-42 from Network via Microsoft Defender
-  Disable User Account jdoe@contoso.com and forced password reset
-  Blocked dropbox.com at firewall/proxy
-  Collected forensic image of device for further analysis
-  Opened Ticket with HR for insider threat review


## 6 Lessons Learned/Recommendation
-  Implement DLP policy to block upload of .zip files > 100MB to external sites
-  Enable alerts for > 1Gb outbound transfer in 10 minutes
-  Maintain an Approved cloud storage whitelist





