# Incident 7 — SOC205: Malicious Macro Executed

## 7.1 Incident Summary
- **Incident Name/ID:** SOC205 – Malicious Macro Executed  
- **Event ID:** 231  
- **Severity:** Medium  
- **Date/Time:** Feb 28, 2024, 08:42 AM  
- **Category:** Malware (Macro Execution)  
- **Affected Host:** Jayne  
- **Host IP:** 172.16.17.198  
- **Operating System:** Windows 10  

---

## 7.2 Alerts, Logs, and Evidence

### **Alert Details**
- File executed: **edit1-invoice.docm**  
- File path: `C:\Users\LetsDefend\Downloads\edit1-invoice.docm`  
- File hash (SHA256):  1a819d18c9a9de4f81829c4cd55a17f767443c22f9b30ca953866827e5d96fb0
- AV/EDR Action: **Detected**  
- Delivered via email attachment inside a password‑protected ZIP (`edit1-invoice.docm.zip`)  

### **Email Investigation**
- **Sender:** jake.admin@cybercommunity.info  
- **Recipient:** jayne@letsdefend.io  
- **Subject:** February Membership Fee  
- Attachment: `edit1-invoice.docm.zip`  
- ZIP password: **infected** (common malware evasion technique)  

### **File Reputation (VirusTotal)**
- **33/68 vendors** flagged the file as malicious  
- Threat labels included:  
- Trojan Downloader  
- VBA.Logan  
- PowerShell Trojan Downloader  

### **Macro Behavior**
- Document contains **VBA AutoOpen macros**  
- Capable of silently executing commands  
- Designed to run PowerShell scripts to download additional malware  
- No secondary payload observed during this investigation  

### **Endpoint Activity**
- ZIP file downloaded to `Downloads` folder  
- File extracted  
- `WINWORD.EXE` opened the DOCM file  
- No suspicious processes or outbound connections detected after execution  

---

## 7.3 Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| **File Name** | edit1-invoice.docm |
| **File Hash (SHA256)** | 1a819d18c9a9de4f81829c4cd55a17f767443c22f9b30ca953866827e5d96fb0 |
| **Sender Email** | jake.admin@cybercommunity.info |
| **Host** | Jayne |
| **Internal IP** | 172.16.17.198 |

---

## 7.4 Root Cause, Attack Vector, and Impact

### **Root Cause**
User received a phishing email containing a **malicious macro-enabled Word document** inside a password‑protected ZIP file.

### **Attack Vector**
Email attachment → ZIP → DOCM → macro execution.

### **Impact**
- Malicious macro executed  
- No additional malware execution observed  
- No lateral movement  
- No privilege escalation  
- **Impact Level:** Medium  

---

## 7.5 Tools and Techniques Used
- Email Security  
- Endpoint Security  
- Log Management  
- Threat Intelligence  
- VirusTotal  
- Case Management  
*(Sandbox not used)*  

---

## 7.6 Screenshots (Placeholders)


![Incident 5 – Email Details](images/incident5-email.png)
![Incident 5 – File Creation Log](images/incident5-file-created.png)
![Incident 5 – Macro Execution Alert](images/incident5-macro-alert.png)
![Incident 5 – VirusTotal Results](images/incident5-virustotal.png)

---

## 7.7 Detailed Investigation Notes
### Timeline
- 08:12 AM — Email delivered to Jayne
- 08:41 AM — ZIP file downloaded
- 08:42 AM — DOCM file executed
- AV/EDR triggered macro execution alert
- No further malicious activity detected

### Analyst Observations
- Password‑protected ZIP used to bypass email scanning
- Macro designed to run PowerShell commands
- No evidence of payload download or system compromise
- User interaction was required for execution
- Sender domain appears suspicious and unrelated to LetsDefend

---

## 7.8 Conclusion
- This was a true positive malicious macro execution incident.
- The macro-enabled document was detected and blocked before causing further harm.
- No additional malware or lateral movement was observed.
- User awareness and macro restrictions are recommended to prevent recurrence.
