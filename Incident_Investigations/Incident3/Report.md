
# Incident 3 — Quishing Attack (QR Code Phishing)
### SOC251 — QR‑Based Phishing Attempt

---

## 1. Incident Summary & Type

- **Incident ID:** SOC251 – Quishing Detected  
- **Event ID:** 214  
- **Severity:** Medium  
- **Date/Time:** Jan 01, 2024 — 12:37 PM  
- **Category:** QR Code Phishing (Quishing)  
- **Recipient:** claire@letsdefend.io  
- **Sender:** security@microsecmfa.com  
- **SMTP Source IP:** 158.69.201.47  
- **Device Action:** Allowed (email reached inbox)

![Incident 3 – Alert Details](1.png)

**Summary:**  
A phishing email impersonating a mandatory MFA update was delivered to the user. The email contained a **malicious QR code** that redirected to a phishing site hosted on IPFS. The user scanned the QR code, increasing the risk of credential theft. The host was isolated as part of containment.

---

## 2. Tools & Features Used (LetsDefend.io)

- Email Security  
- Threat Intelligence  
- Log Analysis  
- VirusTotal  
- CyberChef (QR decoding)  
- Endpoint Monitoring (host isolation)  
- Case Management  

---

## 3. Step-by-Step Investigation Process

### 3.1 Review Alert Details
- Alert triggered by **SOC251 – Quishing Detected**.  
- Email impersonated a **mandatory MFA security update**.  
- Contained a QR code instructing the user to “enable 2FA”.  
- User **opened the email and scanned the QR code**.  
- Host was later **isolated**.

### 3.2 Analyze Email Content
- Social engineering theme: “New Year’s Mandatory Security Update”.  
- Sender domain **microsecmfa.com** is suspicious and unrelated to LetsDefend.  
- No attachments or clickable links — **QR code was the attack vector**.

![Incident 3 – Email Content](5.png)



### 3.3 QR Code Analysis
- QR code decoded using **CyberChef**.  
- URL extracted:  
  `https://ipfs.io/ipfs/Qmbr8wmr41C35c3K2GfiP2F8YGzLhYpKpb4K66KU6mLmL4#`  
- **10/95 vendors flagged the URL as malicious**.  
- Hosted on **IPFS**, commonly abused for phishing.  
- HTTP status: **410 Gone** (content removed but previously malicious).

![Incident 3 – QR Code Decoded](6.png)

### 3.4 Threat Intelligence Findings
- **SMTP IP: 158.69.201.47**  
  - ASN: OVH SAS (Canada)  
  - 9 vendors flagged as malicious/phishing  
- **URL Hosting IP: 209.94.90.1**  
  - ASN: Protocol Labs (IPFS)  
  - Reported 487 times  
  - Known for hosting phishing content  

### 3.5 Network & Log Evidence
- SMTP traffic: **158.69.201.47 → 172.16.20.3 (port 25)**  
- Raw logs confirm sender, subject, and delivery.  
- Endpoint logs show **no malware execution**.  
- Host was isolated as a precaution.

---

## 4. Key Findings & IOCs

### 4.1 Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| **Sender Email** | security@microsecmfa.com |
| **Recipient Email** | claire@letsdefend.io |
| **SMTP Source IP** | 158.69.201.47 |
| **URL from QR Code** | https://ipfs.io/ipfs/Qmbr8wmr41C35c3K2GfiP2F8YGzLhYpKpb4K66KU6mLmL4# |
| **URL Hosting IP** | 209.94.90.1 |
| **ASN (SMTP IP)** | AS16276 (OVH SAS) |
| **ASN (URL Host)** | AS40680 (Protocol Labs) |
| **Threat Tags** | phishing, malicious, quishing |

### 4.2 Evidence Summary
- Malicious QR code leading to phishing URL.  
- User scanned the QR code → increased risk.  
- IPFS hosting used to evade traditional URL filtering.  
- Host isolated to prevent further compromise.

---

## 5. Root Cause, Attack Vector & Impact

### 5.1 Root Cause
User received and interacted with a **malicious QR code** embedded in a phishing email.

### 5.2 Attack Vector
QR code impersonating an MFA security update.

### 5.3 Impact
- User scanned malicious QR code.  
- URL confirmed as phishing.  
- No credential theft confirmed, but **high risk**.  
- Host isolated and email removed.  
- **Impact Level:** Medium.

---

## 7. Timeline

- **12:00 PM** — Email delivered  
- **12:37 PM** — SOC251 alert triggered  
- User opened email and scanned QR code  
- URL resolved to malicious IPFS link  
- Host isolated  
- Email removed  
- Case marked as True Positive  

---

## 8. Analyst Observations

- Attack used **QR code phishing (quishing)** to bypass link scanners.  
- Sender domain spoofed to appear security‑related.  
- IPFS hosting used to evade detection.  
- User interaction increased risk, but containment was effective.  
- No malware executed on endpoint.

---

## 9. Conclusion & Resolution

### Conclusion
This was a **true positive quishing attack**.  
The user scanned a malicious QR code leading to a phishing URL.  
Security controls and analyst intervention prevented further compromise.

### Resolution Steps
- Host isolated.  
- Email removed from mailbox.  
- User advised on phishing awareness.  
- Monitoring for similar campaigns recommended.
