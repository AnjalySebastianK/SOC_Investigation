# Incident 8 — SOC210: Possible Brute Force Detected on VPN

## 8.1 Incident Summary
- **Incident Name/ID:** SOC210 – Possible Brute Force Detected on VPN  
- **Event ID:** 162  
- **Severity:** High  
- **Date/Time:** Jun 21, 2023, 01:51 PM  
- **Category:** Brute Force Attack  
- **User Account:** mane@letsdefend.io  
- **Affected Host:** Mane (Windows 10, IP: 172.16.17.210)

---

## 8.2 Alerts, Logs, and Evidence

### **Alert Details**
- The SOC monitoring system triggered an alert indicating a **possible brute force attack against the VPN service**.
- Multiple login attempts were observed from the same external IP address.
- The attacker attempted to authenticate with several usernames before successfully logging in.
- Source IP Address: **37.19.221.229**
- Destination: **vpn-letsdefend.io (33.33.33.33)**
- Protocol: **HTTPS (Port 443)**

The alert was triggered because a **successful login occurred shortly after several failed login attempts from the same IP address**, which indicates a possible credential-guessing or brute force attack.

---

### **Log Evidence**

**Authentication Logs**

Several failed login attempts were observed before the successful login.

Example logs:

| Time | Source IP | Username | Result |
|-----|-----------|----------|--------|
| 01:43 PM | 37.19.221.229 | sane@letsdefend.io | User name does not exist |
| 01:47 PM | 37.19.221.229 | mane@letsdefend.io | Password incorrect |
| 01:51 PM | 37.19.221.229 | mane@letsdefend.io | Login Successful |

This pattern strongly suggests **credential guessing activity**.

---

**Firewall Logs**

Firewall logs confirm repeated connections from the same source IP.

| Source IP | Source Port | Destination | Destination Port |
|-----------|-------------|-------------|------------------|
| 37.19.221.229 | 1234 | 33.33.33.33 | 443 |
| 37.19.221.229 | 3548 | 33.33.33.33 | 443 |
| 37.19.221.229 | 45045 | 33.33.33.33 | 443 |

These logs indicate repeated connection attempts to the VPN service.

---

**Threat Intelligence**

Threat intelligence lookup shows:

- IP Address: **37.19.221.229**
- ASN: **AS212238**
- ISP: **Datacamp Limited**
- Country: **United States**
- Usage Type: **Data Center / Hosting**

Although no antivirus vendors flagged the IP as malicious, **abuse reports indicate previous suspicious activities such as brute force attempts, port scanning, and web attacks**.

---

**Endpoint Information**

Host details:

- Hostname: **Mane**
- Domain: **LetsDefend**
- IP Address: **172.16.17.210**
- Operating System: **Windows 10 (64-bit)**
- Client Type: **Client Device**

The host was **isolated to prevent further compromise**.

---

## 8.3 Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| **IP Address** | 37.19.221.229 |
| **Destination IP** | 33.33.33.33 |
| **Domain** | vpn-letsdefend.io |
| **Attack Type** | VPN Brute Force |
| **Protocol** | HTTPS |
| **Destination Port** | 443 |

---

## 8.4 Root Cause, Attack Vector, and Impact

### **Root Cause**
The incident occurred due to **multiple credential-guessing attempts against the VPN login portal**, eventually resulting in a successful login.

### **Attack Vector**
Public-facing **VPN login portal over HTTPS (port 443)**.

The attacker attempted authentication with different usernames and passwords until a correct credential was identified.

### **Impact**

- Unauthorized login to the VPN account **mane@letsdefend.io**
- Potential access to internal resources
- Risk of lateral movement within the network
- System required containment and credential reset

**Impact Level:** High

---

## 8.5 Tools and Techniques Used

During the investigation, the following tools and modules were used:

- Monitoring Dashboard
- Log Management System
- Firewall Logs
- Authentication Logs
- Threat Intelligence Lookup
- AbuseIPDB Reputation Check
- Endpoint Security Module
- Case Management System

---

## 8.6 Screenshots 

Insert screenshots for:

- SOC210 alert details
- Authentication logs showing failed logins
- Successful login event
- Firewall connection logs
- Threat intelligence lookup for IP
- AbuseIPDB report
- Endpoint security information

---

## 8.7 Detailed Investigation Notes

### **Timeline**

- **01:43 PM** — Failed login attempt using username **sane@letsdefend.io**
- **01:47 PM** — Failed login attempt using username **mane@letsdefend.io**
- **01:51 PM** — Successful login to VPN using **mane@letsdefend.io**
- **01:51 PM** — SOC210 alert triggered for possible brute force attack

---

### **Analyst Observations**

- Multiple authentication failures occurred from the same external IP.
- The attacker attempted different usernames, suggesting **credential enumeration**.
- A successful login occurred shortly after several failed attempts, indicating a **successful brute force attack**.
- The IP address belongs to a **data center hosting provider**, which is commonly used by attackers.
- Abuse reports indicate prior suspicious activity associated with this IP.

---

## 8.8 Conclusion

This incident is classified as a **True Positive brute force attack**.

The attacker performed multiple login attempts against the VPN portal and eventually succeeded in accessing the account **mane@letsdefend.io**. Because the successful login followed several failed authentication attempts from the same IP address, it strongly indicates a brute force attack.

Immediate response actions included:

- **Isolating the affected host**
- **Resetting user credentials**
- **Blocking the malicious IP address**
- **Monitoring for further suspicious activity**

No evidence of further malicious activity or lateral movement was identified after containment.
