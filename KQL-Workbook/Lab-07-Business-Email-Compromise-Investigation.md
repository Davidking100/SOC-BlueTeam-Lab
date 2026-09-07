Goal: CEO Impersonation and BEC hunting
```
// Query 7.1: Hunt emails from typo-squat domain

EmailEvents
| where SenderFromDomain == "contoso-ceo.com" // REPLACE
| project TimeGenerated, SenderFromAddress, RecipientEmailAddress, Subject, UrlCount, AttachmentCount

// Query 7.2: Who clicked malicious links

EmailUrlInfo
| where SenderFromDomain == "contoso-ceo.com" // REPLACE
| summarize Clicks=count() by RecipientEmailAddress, Url, ClickTime, IsClicked

// Query 7.3: BEC Alerts

AlertInfo
| where Title contains "impersonation" or Title contains "BEC" or Title contains "business email"
