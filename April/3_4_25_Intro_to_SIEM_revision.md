# SIEM (Security Information and Event Management) - Summary

SIEM is a tool that collects, stores, correlates, and analyzes security data from across a network, providing centralized monitoring, alerting, and visibility.

---

## 📊 Log Sources

### 1. **Host-Centric Log Sources**
- Capture events on individual endpoints.
- Examples:
  - Windows Event Logs
  - Sysmon
  - Osquery

#### Common Events:
- File access
- Authentication attempts
- Process execution
- Registry modifications
- PowerShell execution

### 2. **Network-Centric Log Sources**
- Capture communication between hosts or with external networks.
- Protocols: SSH, VPN, HTTP/S, FTP

#### Common Events:
- SSH sessions
- FTP file access
- VPN usage
- Web traffic
- Network file sharing

---

## 🧠 Key SIEM Features
- Real-time log ingestion
- Abnormal activity alerting
- 24/7 monitoring and visibility
- Early threat detection
- Data insights and visualization
- Historical investigations

---

## 🖥 OS-Specific Logging

### Windows
- Logs viewable via **Event Viewer**
- Events have unique IDs (e.g., 4688 for process execution)

### Linux
- Logs stored in `/var/log/`
  - `/var/log/httpd` – HTTP logs
  - `/var/log/cron` – Cron jobs
  - `/var/log/auth.log` / `/var/log/secure` – Auth logs
  - `/var/log/kern` – Kernel events

---

## 📥 Log Collection Methods

1. **Agent/Forwarder**  
   - Lightweight tool that forwards logs to SIEM (e.g., Splunk Forwarder)

2. **Syslog**  
   - Standard protocol for centralized logging

3. **Manual Upload**  
   - Offline data ingestion for analysis (Splunk, ELK)

4. **Port-Forwarding**  
   - Endpoints send data to SIEM on specific ports

---

## 🧩 Capabilities of SIEM
- Event correlation
- Host and network visibility
- Threat hunting
- Incident investigation and response

---

## 👨‍💻 Analyst Responsibilities
- Monitor and investigate alerts
- Triage false positives
- Tune noisy rules
- Report for compliance
- Detect visibility blind spots

---

## 📈 Dashboards
- Visual representation of data and alerts
- Info included:
  - Alert highlights
  - Failed login attempts
  - Ingested event count
  - Top domains visited

---

## 🧩 Correlation Rules

Logical expressions to detect malicious behavior:

### Examples:
- **Multiple Failed Logins**: 5 failures in 10 seconds → Alert
- **Successful Login After Failures**
- **USB Insertion Alert**
- **Outbound traffic > 25 MB** → Possible Data Exfiltration

---

## 📌 Use Cases

### Use Case 1: Log Clearing
- **Event ID**: 104
- **Rule**: If Log source is WinEventLog AND EventID is 104 → Trigger alert

### Use Case 2: Whoami Execution
- **Event ID**: 4688
- **Rule**: If Log Source is WinEventLog AND EventCode is 4688 AND NewProcessName contains "whoami" → Trigger alert

---

## 🔎 Alert Investigation

Upon alert:
- Check associated logs
- Identify if it’s a **True Positive** or **False Positive**
- Actions:
  - Tune rules for false positives
  - Investigate further
  - Contact asset owner
  - Isolate infected system
  - Block malicious IP

---
