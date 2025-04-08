# Task : Identify and Investigate an Infected Host

## Scenario Overview
An alert from the client’s IDS indicated a suspicious process on an HR department host. Tools related to network information gathering and scheduled tasks were used. Event logs (Event ID: 4688) were collected and ingested into **Splunk** (index: `win_eventlogs`) for further investigation.

### Network Segmentation
- **IT Department**: James, Moin, Katrina  
- **HR Department**: Haroon, Chris, Diana  
- **Marketing Department**: Bell, Amelia, Deepak

---

## Investigation Findings

### 2.1 Logs from March 2022
**Answer**: `13959`

### 2.2 Imposter User Account
- Used Splunk query:  
  `index=win_eventlogs | top limit=11 UserName`
- **Answer**: `Amel1a`

### 2.3 Scheduled Task Executed by HR User
- Used Splunk query:  
  `index=win_eventlogs schtasks`
- Checked `CommandLine` field
- **Answer**: `Chris.fort`

### 2.4 HR User Who Executed LOLBIN (certutil) to Download Payload
- Used Splunk query:  
  `index=win_eventlogs HostName="*HR*" | rare limit=20 CommandLine`
- Observed usage of `certutil` to download `benign.exe`
- **Answer**: `haroon`

### 2.5 LOLBIN Used for Payload Download
**Answer**: `certutil.exe`

### 2.6 Date of Binary Execution
**Answer**: `2022-03-04`

### 2.7 Third-Party Site Used for Payload Download
**Answer**: `controlc.com`

### 2.8 Name of Downloaded File
**Answer**: `benign.exe`

### 2.9 Flag Pattern in Malicious File
**Answer**: `THM{KJ&*H^B0}`

### 2.10 URL Accessed by Infected Host
**Answer**: `https://controlc.com/e4d11035`

---

## Conclusion
This task concluded the **Benign Room**.
