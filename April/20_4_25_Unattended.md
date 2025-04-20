![image](https://github.com/user-attachments/assets/8b01f0fc-b671-47a8-9512-1a19acd846f5)


# Digital Forensics Investigation Report

## Task 1: Introduction

A newly hired employee noticed a suspicious janitor leaving his office upon returning from lunch.  
**Objective:** Investigate user activity on **19th November 2022 between 12:05 PM to 12:45 PM**, and determine if files were accessed and exfiltrated.
---

## Task 2: Windows Forensics Review

- Provided: Cheat sheet for registry hive file locations.
---

## Task 3: Snooping Around

Initial findings indicate that the machine was accessed during the specified timeframe.

### Objectives:

- **File type searched:** `.pdf`  
- **Keyword searched:** `continental`  

### Steps:
- Use **Registry Explorer** to open `NTUSER.DAT`:
  - Path:  
    `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`
  - Use **Data Interpreter** under "Strings → Unicode" to find searched terms.

---

## Task 4: Can’t Simply Open It

Attacker downloaded a tool to continue accessing content.

### Objectives:

- **Downloaded file name:** `7z2201-x64.exe`  
- **Download timestamp:** `2022-11-19 12:09:19 UTC`  
- **Opened PNG timestamp:** `2022-11-19 12:10:21`

### Steps:
- Use **Autopsy**:
  - Add data source → Select KAPE `C` folder → Configure Ingest → Select **Recent Activity**
  - Under **Data Artifacts**, check `Web Downloads` for file info.
  - Use Registry to locate the `.png` file (opened shortly after `.exe`).

---

## Task 5: Sending It Outside

Attacker could not use USB, so exfiltration was done online.

### Objectives:

- **Text file opened:** `2` times  
- **Last modified time:** `2022-11-19 12:12:35`  
- **Pastebin URL:** `https://pastebin.com/1FQASAav`  
- **Exfiltrated string:** `ne7AIRhi3pdesy9RnOrN`

### Steps:
- Open Command Prompt as Admin
- Run:
  ```bash
  JLECmd -d C:\Users\THN-RFedora\desktop\kape-results\C\Users\THM-RFedora\
  ```
- Use date/time filters to locate file operations.
- In Autopsy, check Web History to identify pastebin activity and string.
