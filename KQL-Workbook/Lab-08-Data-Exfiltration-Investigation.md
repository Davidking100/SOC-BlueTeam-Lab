Goal: Insider threat and DLP

```Kql
// Query 8.1: Large data uploads to cloud storage

DeviceNetworkEvents
| where ActionType == "ConnectionSuccess"
| where RemoteUrl contains "dropbox.com" or RemoteUrl contains "drive.google.com" or RemoteUrl contains "onedrive"
| where SentBytes > 1000000 // > 1GB
| project TimeGenerated, DeviceName, AccountName, InitiatingProcessFileName, RemoteUrl, SentBytes

// Query 8.2: Sensitive file access and copy

DeviceFileEvents
| where FileName contains "HR" or FileName contains "Finance" or FileName endswith ".zip" or FileName endswith ".rar"
| project TimeGenerated, DeviceName, AccountName, FileName, ActionType, FolderPath
