cat << 'EOF' > QRadar101_README.md
# IBM QRadar 101 Challenge Report

## Challenge Overview

The **QRadar 101 Challenge** is designed to introduce the fundamentals of **Security Information and Event Management (SIEM)** using IBM QRadar. In this challenge, security analysts investigate suspicious activity within an organization's network by analyzing logs collected from multiple sources.

IBM QRadar collects and correlates logs from different systems such as servers, intrusion detection systems, and network devices. These logs allow analysts to detect suspicious activities, investigate potential security incidents, and understand attacker behavior.

This challenge simulates a real-world **SOC (Security Operations Center)** investigation scenario where analysts must identify compromised systems, attacker tools, and malicious activities.

---

# Objectives

The objectives of this challenge were to:

- Learn the basics of the **IBM QRadar SIEM platform**
- Understand how logs are collected and analyzed
- Perform **event correlation and log analysis**
- Investigate suspicious activities in the network
- Identify attacker techniques and compromised systems
- Record findings and document the investigation process

---

# Step-by-Step Methodology

## Step 1: Exploring the QRadar Interface

The investigation began by accessing the QRadar dashboard and familiarizing with its main components.

Important sections include:

- Log Activity
- Network Activity
- Offenses
- Rules
- Admin

These components allow SOC analysts to monitor network events, investigate alerts, and detect security incidents.

---

## Step 2: Reviewing Log Sources

The first step of the investigation involved identifying the **log sources connected to the SIEM system**.

Navigation Path:

Admin → Log Sources

Total log sources identified:

15

Screenshot:

![Log Sources](screenshots/qradar_q1.png)

---

## Step 3: Identifying the Network Monitoring System

During log analysis, an intrusion detection system was identified that monitors network traffic.

IDS Software:

Suricata

Suricata generates alerts when suspicious network activity or known attack signatures are detected.

Screenshot:

![IDS Detection](screenshots/qradar_q2.png)

---

## Step 4: Identifying the Network Domain

Authentication logs revealed the internal domain used by the organization.

Domain Name:

hackdefend.local

Screenshot:

![Domain](screenshots/qradar_q3.png)

---

## Step 5: Investigating Suspicious Network Communication

Further analysis showed that multiple systems were communicating with a suspicious server.

Suspicious IP address identified:

192.168.20.20

This indicated potential malware activity or compromised hosts within the network.

---

## Step 6: Identifying the Attacker

Through event correlation and log investigation, the attacker’s IP address was identified.

Attacker IP:

192.20.80.25

---

## Step 7: Identifying the First Infected Machine

The investigation revealed the first compromised machine in the network.

First infected host:

192.168.10.15

Associated user account:

nour

---

## Step 8: Investigating Malware Activity

The attacker initially infected the system using a malicious document.

Malicious file:

important_instructions.docx

MD5 hash of the file:

9D08221599FCD9D35D11F9CBD6A0DEA3

---

## Step 9: Identifying Persistence Technique

The attacker used a persistence technique mapped to the MITRE ATT&CK framework.

MITRE Technique ID:

T1547.001

This technique allows attackers to maintain persistence through system startup mechanisms.

---

## Step 10: Lateral Movement Detection

Logs revealed that the attacker moved laterally across systems using the following tool:

wmiexec.py

This tool allows attackers to execute commands remotely on other machines in the network.

---

## Step 11: Data Exfiltration Activity

The attacker used the following tool to exfiltrate sensitive data from the network.

Data exfiltration tool:

curl

---

# Summary of Key Findings

| Indicator | Value |
|------|------|
| Log Sources | 15 |
| IDS System | Suricata |
| Domain Name | hackdefend.local |
| Attacker IP | 192.20.80.25 |
| First Infected Machine | 192.168.10.15 |
| Compromised User | nour |
| Lateral Movement Tool | wmiexec.py |
| Data Exfiltration Tool | curl |
| Malicious File | important_instructions.docx |

---

# Key Learnings

This challenge helped develop several important cybersecurity skills:

### SIEM Log Analysis
Understanding how security logs are collected and analyzed using IBM QRadar.

### Event Correlation
Learning how different events across multiple systems can be correlated to identify suspicious activity.

### Threat Investigation
Investigating attacker behavior by analyzing authentication logs, network activity, and system events.

### Incident Response Skills
Reconstructing the attack timeline and identifying compromised systems within the network.

---

# Conclusion

The QRadar 101 Challenge provided practical experience in investigating cyber incidents using a SIEM platform. By analyzing logs from multiple sources, it was possible to identify the attacker, detect compromised systems, and understand how the attacker moved within the network.

This exercise demonstrates how SIEM tools like **IBM QRadar** help SOC analysts monitor network activity, detect threats, and respond to security incidents effectively.

---

# Tools Used

| Tool | Purpose |
|------|------|
| IBM QRadar | SIEM log analysis |
| Suricata IDS | Network intrusion detection |
| Windows Event Logs | System activity monitoring |

EOF
