# Incident 2 — SOC101: Phishing Email Detected

## 2.1 Incident Summary
- **Incident Name/ID:** SOC101 – Phishing Mail Detected  
- **Event ID:** 59  
- **Severity:** Low  
- **Date/Time:** Feb 14, 2021, 03:00 AM  
- **Category:** Phishing Email  
- **Recipient:** mark@letsdefend.io  
- **Sender:** hahaha@ihackedyourcomputer.com  
- **SMTP Source IP:** 27.128.173.81  

![Incident 2 – Alert Details](1.png)

---

## 2.2 Alerts, Logs, and Evidence

### **Alert Details**
- Detection Rule: **SOC101 – Phishing Mail Detected**  
- Email contained **threatening extortion content**.  
- No URLs or attachments present.  
- Device Action: **Blocked**  
- Email was automatically removed from the user’s inbox.

### **Email Content Summary**
- Sender claims to have hacked the user’s computer.  
- Threatens to leak personal files unless payment is made within 3 days.  
- Classic **extortion-style phishing email**.

### **Log Evidence**
- SMTP connection from external IP **27.128.173.81** to internal mail server.  
- Email security logs show the message delivered and then blocked.  
- Email appears in historical logs but is no longer accessible to the user.

### **Threat Intelligence Findings**
- IP **27.128.173.81** belongs to **Chinanet (China Telecom)**.  
- Reputation: **Negative community score (-23)**  
- Multiple files observed embedding this IP, but **vendors classify it as clean** (likely due to non‑malware extortion content).  
- WHOIS confirms ownership by China Telecom, Hebei province.

---

## 2.3 Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| **Sender Email** | hahaha@ihackedyourcomputer.com |
| **Recipient Email** | mark@letsdefend.io |
| **SMTP Source IP** | 27.128.173.81 |
| **Country** | China |
| **ASN** | AS4134 (Chinanet) |
| **Subject** | “I hacked your computer” |

---

## 2.4 Root Cause, Attack Vector, and Impact

### **Root Cause**
A **phishing/extortion email** was sent to an internal user from an external SMTP server.

### **Attack Vector**
Email delivered via **SMTP from external IP 27.128.173.81**.

### **Impact**
- Email was **blocked** by security controls.  
- No user interaction.  
- No malware, no attachments, no URLs.  
- No compromise of internal systems.  
- **Impact Level:** Low  

---

## 2.5 Tools and Techniques Used
- Email Security Module  
- Threat Intelligence  
- Log Analysis  
- VirusTotal  
- Case Management  

---

## 2.6 Screenshots


![Incident 2 – Email Content](5.png)
![Incident 2 – Log](4.png)
![Incident 2 – Closed](7.png)

---
## 2.7 Detailed Investigation Notes

### Timeline
- 03:00 AM — Phishing email received by mark@letsdefend.io
- Email security flagged it as SOC101 – Phishing Mail Detected
- The email was blocked and removed
- Analyst reviewed logs and threat intel
- Confirmed no malicious links or attachments

### Analyst Observations
- Email uses intimidation and extortion tactics.
- No technical indicators of compromise beyond sender IP.
- Sender domain appears intentionally malicious and spoofed.
- IP reputation is poor but not associated with malware distribution.

## 2.8 Conclusion
- This was a true positive phishing/extortion attempt.
- Security controls successfully blocked the email, preventing user exposure.
- No further action required beyond monitoring and user awareness.
