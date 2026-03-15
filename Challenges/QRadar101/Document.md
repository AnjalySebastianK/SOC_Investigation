# QRadar 101 Challenge

## Objective
The **QRadar 101 Challenge** introduced the fundamentals of **Security Information and Event Management (SIEM)** using IBM QRadar. The goal of this exercise was to understand how SOC analysts monitor networks, investigate suspicious activity, and correlate events from multiple log sources to identify security incidents.

This challenge focused on analyzing logs collected from different systems within an organization and reconstructing attacker activity across the network.

---

# Investigation Overview

During the investigation, security logs were analyzed using the QRadar platform to identify suspicious activity and trace the actions of an attacker within the network.

The analysis revealed several key findings:

- Total log sources monitored by the SIEM: **15**
- Network IDS used for monitoring: **Suricata**
- Organization domain identified: **hackdefend.local**
- Attacker IP address: **192.20.80.25**
- First infected machine: **192.168.10.15**
- Compromised user account: **nour**
- The attacker initially gained access through a malicious document: **important_instructions.docx**
- The MD5 hash of the malicious file was: **9D08221599FCD9D35D11F9CBD6A0DEA3**

---

# Attacker Techniques Identified

### Persistence
The attacker used a persistence technique mapped to the MITRE ATT&CK framework: **T1547.001**

This technique allows malicious programs to maintain persistence during system startup.

---

### Lateral Movement
After compromising the first machine, the attacker moved laterally through the network using:**wmiexec.py**

This tool is part of the **Impacket toolkit** and allows attackers to execute commands remotely on other systems.

---

### Data Exfiltration
The attacker used the following tool to exfiltrate data from the compromised system: **curl**

---

# Key Concepts Learned

### SIEM Monitoring
IBM QRadar collects logs from multiple systems including servers, network devices, and security tools to monitor the network for suspicious activity.

### Event Correlation
QRadar correlates multiple security events from different log sources to identify potential threats.

### Log Analysis
Security logs are analyzed to detect anomalies such as unauthorized access, malware execution, or suspicious network communication.

### Rule Creation
Custom detection rules can be created to trigger alerts based on suspicious patterns.

Example detection scenarios include:

- Multiple failed login attempts
- Suspicious external IP communication
- Malware execution alerts
- Data exfiltration attempts

---

# Key Findings

| Indicator | Value |
|------|------|
| Log Sources | 15 |
| IDS Software | Suricata |
| Domain | hackdefend.local |
| Attacker IP | 192.20.80.25 |
| First Infected Host | 192.168.10.15 |
| Compromised User | nour |
| Lateral Movement Tool | wmiexec.py |
| Data Exfiltration Tool | curl |

---

# Skills Developed

- SIEM log analysis
- Event correlation investigation
- Threat detection using QRadar
- Identifying attacker tactics and techniques
- Investigating compromised systems
- SOC incident investigation

---

# Tools Used

| Tool | Purpose |
|----|----|
| IBM QRadar | SIEM monitoring and log analysis |
| Suricata IDS | Network intrusion detection |
| Windows Event Logs | System activity monitoring |
| SIEM Event Correlation | Threat detection |

---

# Conclusion

The QRadar 101 challenge provided hands-on experience in using a SIEM platform to investigate a cybersecurity incident. By analyzing logs from multiple sources, it was possible to identify the attacker, detect compromised systems, and understand how the attacker moved within the network.

This exercise demonstrates the importance of SIEM tools in modern **Security Operations Centers (SOC)** for detecting threats, correlating events, and responding to cyber attacks.

---
