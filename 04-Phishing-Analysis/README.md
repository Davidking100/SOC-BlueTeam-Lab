## Case 04: Phishing Email Triage

**Scenario:** Employee `sarah.k@company.com` reported suspicious email claiming to be from HR Payroll.

### **IOCs Identified**
1. **Sender Domain Spoofing**: `payroll-support@compnay-portal.com` - Typo: "compnay"
2. **Malicious URL**: `http://compnay-portal.com/payroll-login` - HTTP not HTTPS
3. **Social Engineering**: Urgency + Threat "payroll suspension"

### **Risk Rating: HIGH**
Credential harvesting phishing.

### **MITRE ATT&CK Mapping**
- **T1566.001 - Phishing: Spearphishing Link**
- **T1204.001 - User Execution: Malicious Link**

### **Response Actions**
1. Block sender domain at email gateway
2. Delete email from mailbox + org-wide search
3. Notify user + send org-wide alert
4. Submit URL to VirusTotal
5. Create email rule for payroll + urgent + external domains
