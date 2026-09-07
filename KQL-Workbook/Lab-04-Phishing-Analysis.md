Goal: Email authentication and header Analysis

```Kql
// Query 4.1: Check SPF/DKIM/DMARC for domain

EmailEvents
| where SenderFromAddress contains "contoso"
| project TimeGenerated, SenderFromAddress, RecipientEmailAddress, SPF, DKIM, DMARC, EmailAction, Subject
| order by TimeGenerated desc

// Query 4.2: Find emails that failed authentication

EmailEvents
| where DMARC == "Fail" or SPF == "Fail" or DKIM == "Fail"
| summarize FailedEmails=count() by SenderFromAddress, DMARC, SPF, DKIM
