# Incident 10 — SOC170: Passwd Found in Requested URL – Possible LFI Attack

## 10.1 Incident Summary
- **Incident Name/ID:** SOC170 – Passwd Found in Requested URL – Possible LFI Attack  
- **Event ID:** 120  
- **Severity:** High  
- **Date/Time:** Mar 01, 2022, 10:10 AM  
- **Category:** Web Attack / Local File Inclusion (LFI)  
- **User Account:** N/A  
- **Affected Host:** WebServer1006 (IP: 172.16.17.13)

---

## 10.2 Alerts, Logs, and Evidence

### **Alert Details**
The monitoring system detected a suspicious web request containing the string **"/etc/passwd"** in the URL, which is commonly used in **Local File Inclusion (LFI) attacks**.

Key alert information:

- **Source IP:** 106.55.45.162  
- **Destination IP:** 172.16.17.13  
- **HTTP Request Method:** GET  
- **Requested URL:** https://172.16.17.13/?file=../../../../etc/passwd
- **User-Agent:** Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)

The alert was triggered because the requested URL contained **"passwd"**, indicating a possible attempt to read sensitive system files from the Linux server.

---

### **Log Evidence**

**Firewall / Web Logs**

| Source IP | Source Port | Destination IP | Destination Port | Method |
|-----------|-------------|---------------|------------------|-------|
| 106.55.45.162 | 49028 | 172.16.17.13 | 443 | GET |

Additional request details:
Request URL: https://172.16.17.13/?file=../../../../etc/passwd

Device Action: Allowed

This indicates that the request reached the server.

---

**HTTP Response Analysis**

Further log analysis shows that the request generated an **HTTP 500 response code**.

Key observations:

- HTTP Status Code: **500**
- Response Size: **0**

This means the request was **not processed successfully by the web application**.

Therefore, the attacker was **unable to retrieve the /etc/passwd file**.

---

**Threat Intelligence**

Source IP reputation analysis:

- **IP Address:** 106.55.45.162  
- **ASN:** AS45090  
- **Organization:** Shenzhen Tencent Computer Systems Company Limited  
- **Country:** China  

No major security vendors flagged this IP as malicious, but the request pattern indicates **web vulnerability scanning activity**.

---

## 10.3 Indicators of Compromise (IOCs)

| Type | Value |
|------|------|
| **Source IP** | 106.55.45.162 |
| **Destination IP** | 172.16.17.13 |
| **Requested File** | /etc/passwd |
| **Attack Technique** | Local File Inclusion (LFI) |
| **HTTP Method** | GET |
| **User Agent** | Mozilla/4.0 (MSIE 6.0 compatible) |

---

## 10.4 Root Cause, Attack Vector, and Impact

### **Root Cause**
The alert was triggered due to a malicious HTTP request attempting to exploit a **Local File Inclusion (LFI) vulnerability** in the web application.

### **Attack Vector**
External attacker sending a crafted **HTTP GET request** targeting a vulnerable web parameter: file=../../../../etc/passwd

This technique attempts to traverse directories and access sensitive system files.

### **Impact**

- The request reached the web server.
- The server returned **HTTP 500 (Internal Server Error)**.
- The sensitive file **/etc/passwd was not accessed**.
- No evidence of successful exploitation was identified.

**Impact Level:** Low

---

## 10.5 Tools and Techniques Used

The following tools and systems were used during the investigation:

- Monitoring Dashboard
- Log Management System
- Firewall Logs
- Web Server Logs
- Threat Intelligence Lookup
- Case Management System

---

## 10.6 Screenshots (Placeholders)

Insert screenshots for:

- SOC170 alert details
- HTTP request logs
- Requested URL containing `/etc/passwd`
- Firewall connection logs
- Threat intelligence lookup
- Log analysis showing HTTP 500 response

---

## 10.7 Detailed Investigation Notes

### **Timeline**

- **10:10 AM** — Suspicious HTTP request detected from IP **106.55.45.162**  
- **10:10 AM** — Request attempted directory traversal to access `/etc/passwd`  
- **10:10 AM** — Web server returned **HTTP 500 response**  
- **10:11 AM** — SOC170 alert generated for possible LFI attack

---

### **Analyst Observations**

- The request clearly indicates a **directory traversal attempt**.
- Attackers often attempt to access **/etc/passwd** to enumerate system users.
- The request was likely part of an **automated vulnerability scan**.
- Since the server returned **HTTP 500**, the request was not executed successfully.
- No sensitive data exposure was detected.

---

## 10.8 Conclusion

This incident is classified as a **True Positive LFI attack attempt**.

An attacker attempted to exploit a potential Local File Inclusion vulnerability by requesting the **/etc/passwd** file through a crafted URL. However, the web application returned an **HTTP 500 error**, indicating that the request was not successfully processed.

As a result:

- The attack **was unsuccessful**
- No sensitive information was exposed
- No system compromise occurred

Therefore, **no escalation or endpoint containment was required**, but monitoring and web application hardening are recommended.
