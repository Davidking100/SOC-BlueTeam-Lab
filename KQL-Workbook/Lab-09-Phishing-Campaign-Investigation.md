Goal: Invoice phishing and email purge tracking 
```Kql

// Query 9.1: Find phishing campaign emails

EmailEvents
| where SenderFromAddress == "billing@contoso-invoice.com" // REPLACE
| project TimeGenerated, Subject, RecipientEmailAddress, EmailAction, DeliveryLocation

// Query 9.2: Track URL clicks from campaign

EmailUrlInfo
| where Url contains "contoso-invoice-secure.fake" // REPLACE
| project RecipientEmailAddress, Url, ClickTime, IsClicked

// Query 9.3: Check if email was purged

EmailEvents
| where NetworkMessageId == "REPLACE-WITH-MESSAGEID"
| project DeliveryAction, DeliveryLocation, Subject
