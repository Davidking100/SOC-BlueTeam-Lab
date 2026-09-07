Goal: Detect RDP and SSH brute force attacks

```Kql
// Query 6.1: RDP Brute Force - 5+ failed logins in 5 minutes

SecurityEvent
| where EventID == 4625 // Failed Logon
| where LogonType == 10 // RDP
| summarize FailedAttempts=count() by TargetAccount, IpAddress, bin(TimeGenerated, 5m)
| where FailedAttempts >= 5
| order by FailedAttempts desc

// Query 6.2: SSH Brute Force - Linux

Syslog
| where Facility == "auth" 
| where SyslogMessage contains "Failed password"
| parse SyslogMessage with * "from " IpAddress *
| summarize Attempts=count() by IpAddress, bin(TimeGenerated, 10m)
| where Attempts >= 10
```

