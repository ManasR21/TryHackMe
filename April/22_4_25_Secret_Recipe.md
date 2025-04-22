# Windows Registry Forensics Investigation: Coffely Case

## 🕵️‍♂️ Case Summary:
Jasmine, owner of the renowned New York coffee shop *Coffely*, suspects James from the IT department of copying her secret recipe file during a laptop repair. His machine was confiscated and analyzed through Windows Registry artifacts. This document summarizes the forensic findings.

---

## 🖥️ System Information

- **Computer Name:** `JAMES`  
  *(Location: SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName)*

- **Administrator Account Creation Date:** `2021-03-17 14:58:48`  
  *(Location: SAM\Domains\Account\Users)*

- **Administrator RID:** `500`  
  *(RID is the last segment of the SID for Administrator account)*

- **Number of User Accounts:** `7`  
  *(Check: Names folder under SAM hive)*

---

## 🧑‍💻 Suspicious Activity

- **Suspicious Backdoor Account RID 1013:** `bdoor`

- **VPN Used:** `ProtonVPN`  
  *(Found in SOFTWARE Hive: NetworkList)*

- **First VPN Connection Timestamp:** `2022-10-12 19:52:36`

- **Last DHCP IP Address Assigned:** `172.31.2.197`  
  *(Location: SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces)*

---

## 📁 File & Command Access

- **Third Shared Folder Path:** `C:\RESTRICTED FILES`  
  *(Search for 'shared' in registry explorer)*

- **Secret Recipe File Name:** `secret-recipe.pdf`  
  *(RecentDocs in NTUSER.DAT hive)*

- **Command to Enumerate Network Interfaces:**  
  `pnputil /enum-interfaces`  
  *(Run history from NTUSER.DAT)*

- **Searched Network Transfer Tool:** `netcat`  
  *(Explorer search history - WordWheelQuery)*

- **Recently Opened Text File:** `secret-code.txt`  
  *(RecentDocs in NTUSER.DAT)*

---

## ⚙️ Executable Usage & Monitoring

- **Number of PowerShell Executions:** `3`  
  *(NTUSER.DAT\...\UserAssist)*

- **Executed Network Monitoring Tool:** `wireshark`

- **ProtonVPN Execution Time:** `343 seconds`  
  *(Activity time recorded in registry)*

- **Path of `Everything.exe`:**  
  `C:\Users\Administrator\Downloads\tools\Everything\Everything.exe`

---

## 📌 Conclusion:
Evidence from the registry strongly suggests that James:
- Created a backdoor account (`bdoor`)
- Used ProtonVPN for concealment
- Accessed `secret-recipe.pdf`
- Used tools like `netcat`, `wireshark` for reconnaissance and potential exfiltration.

