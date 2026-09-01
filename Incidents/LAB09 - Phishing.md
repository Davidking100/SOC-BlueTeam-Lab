### **File 2: `Incidents/LAB09-Phishing.md`**

# LAB 09: Phishing Email Investigation

## 1. Incident Details
**Incident ID:** INC-2026-08-009
**Date/Time Detected:** 2026-08-19 01:13:00 UTC
**Date/Time Contained:** 2026-08-19 01:25:00 UTC
**Classification:** True Positive
**Severity:** Medium
**Analyst:** David Oluwatosin
**Status:** Closed
**Data Sources:** Microsoft Defender XDR - EmailEvents, EmailUrlInfo

## 2. Summary
Defender for Office 365 flagged a phishing email impersonating Contoso Billing. 1 user clicked the malicious link. 3 additional users received the email.

## 3. Timeline - 5 W's
- **What:** Phishing email with malicious login link
- **When:** 2026-08-19 01:13:00 UTC
- **Where:** Microsoft 365, Exchange Online
- **Who:** Victims: `sara@contoso.com` + 3 others. Sender: `billing@contoso-invoice.com`
- **How:** User clicked URL: `http://contoso-invoice-secure.fake/login`. ThreatType: Phish

## 4. Investigation Steps
  kql
// Step 1: Find who clicked the malicious URL
EmailUrlInfo
| where TimeGenerated > ago(24h)
| where Url contains "contoso-invoice-secure.fake"
| summarize ClickCount = count() by RecipientEmailAddress, Url

// Step 2: Find all recipients of the message
EmailEvents
| where Subject contains "Invoice" and SenderFromAddress == "billing@contoso-invoice.com"
| summarize Recipients = dcount(RecipientEmailAddress) 


**Findings**:
  1. 4 Total recipients identified
  2. 1 User clicked: sara@contoso.com
  3. Malicious domain uses typo-squatting of contoso-invoice


 ## 5. Containment & Remediation Actions
  . Isolated user sara@contoso.com and 3 recipient in Microsoft Defender
  . Reset passwords and revoked all active session for 4 users 
  . Purged malicious email from all 4 mail boxes using "Hard Delete"
  . Added contoso-invoice-secure.fake to URL block list
  . Reported sender domain to Microsoft Defender 


## 6. Lessons Learned / Recommendation 
  . Enable Impersonation protection for contoso.com in Anti-phishing policy
  . Run quarterly phishing simulation and security awareness training
  . Create transport rule to quarantine external emails with "invoice" in subject 


## Evidence 
  Email Header Analysis, EmailUrlinfo Screenshot, Email Purge Confirmation


