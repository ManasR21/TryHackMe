# Sysmon Overview

## What is Sysmon?
- A Windows system service and driver that logs detailed system activity for security analysis.
- Used with SIEM tools for detecting malicious activity.

### Where are logs stored?
- **Event Viewer Path:** `Applications and Services Logs/Microsoft/Windows/Sysmon/Operational`

### Configuration:
- Uses XML config files to define what events to monitor.
- Two popular configs:
  - **SwiftOnSecurity** (exclusion-based)
  - **ION-Storm** (inclusion-based)

## Key Event IDs in Sysmon
- **Process Creation (ID 1)** – Detects suspicious process executions.
- **Network Connection (ID 3)** – Logs remote network connections.
- **Image Loaded (ID 7)** – Tracks DLL injections/hijacking.
- **CreateRemoteThread (ID 8)** – Monitors process injection techniques.
- **File Created (ID 11)** – Detects file creations (useful for ransomware detection).
- **Registry Changes (ID 12-14)** – Tracks persistence techniques.
- **FileCreateStreamHash (ID 15)** – Monitors alternate data streams for hidden malware.
- **DNS Queries (ID 22)** – Helps filter and detect malicious domains.

## Installing & Running Sysmon
### Install Sysmon from Sysinternals
```powershell
Download-SysInternalsTools C:\Sysinternals
```

### Run Sysmon with a config file:
```powershell
Sysmon.exe -accepteula -i ..\Configuration\swift.xml
```

### View logs in Event Viewer
- Open `Event Viewer` → Navigate to `Sysmon/Operational`

## Filtering & Hunting Suspicious Events
### Best Practices:
- **Exclude > Include** – Reduces noise by filtering out normal activity.
- **Use CLI over GUI** – PowerShell (`Get-WinEvent`) provides better control.
- **Know Your Environment** – Understand normal vs. suspicious behavior.

### Filtering in Event Viewer
- Use **Filter Current Log** to filter by **Event ID** and **Keywords**.

### Filtering with PowerShell:
```powershell
Get-WinEvent -Path <Path to Log> -FilterXPath '*/System/EventID=<ID>'
```

### Example: Find network connections on port 4444
```powershell
Get-WinEvent -Path C:\Logs\sysmon.evtx -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=4444'
```

## Practical Questions Answered
- **How many Event ID 3 events in Filtering.evtx?** → `73,591`
- **UTC time of first Event ID 3 in Filtering.evtx?** → `2021-01-06 01:35:50.464`

## Detecting Metasploit Activity
- Look for suspicious network connections (e.g., ports **4444, 5555**).
- Monitor process injection techniques (**CreateRemoteThread – Event ID 8**).
- Use Sysmon logs to detect **Meterpreter payloads** and **C2 beacons**.



# Task 6: Detecting Mimikatz

## Overview
Mimikatz is a well-known post-exploitation tool used to dump credentials from memory, primarily by targeting the LSASS (Local Security Authority Subsystem Service) process. Attackers may attempt to bypass traditional antivirus (AV) defenses using obfuscation, droppers, or execution from an elevated process.

## Detection Methods

### File Creation Monitoring
- Simple but effective technique: Look for files named `Mimikatz.exe` that may have bypassed AV.
- Less effective against advanced threats using renamed or obfuscated versions.

### Hunting Abnormal LSASS Behavior
- **ProcessAccess Event ID 10 (Sysmon):** Monitor when LSASS is accessed by any process other than `svchost.exe`.
- **Filtering Out Noise:** Modify configurations to exclude expected behaviors (e.g., `svchost.exe` accessing LSASS).
- **Viewing Attack Logs:** Open `Hunting_LSASS.evtx` in Event Viewer to analyze an obfuscated Mimikatz attack.

### PowerShell Detection
Use `Get-WinEvent` with XPath queries to filter LSASS access attempts:
```powershell
Get-WinEvent -Path <Path to Log> -FilterXPath '*/System/EventID=10 and */EventData/Data[@Name="TargetImage"] and */EventData/Data="C:\Windows\system32\lsass.exe"'
```
- Helps in quick identification of potential credential dumping attempts.

---

# Task 7: Hunting Malware

## Overview
Malware detection focuses on RATs (Remote Access Trojans) and backdoors, which provide attackers remote access to a system. These threats often employ stealth mechanisms to evade traditional security solutions.

## Detection Methods

### Hunting RATs and C2 Servers
- Focus on identifying suspicious open ports used by RATs (e.g., 1034, 1604, 8080).
- Modify configuration files to exclude common network connections (e.g., OneDrive) while still capturing relevant anomalies.
- **Viewing Attack Logs:** Open `Hunting_Rats.evtx` in Event Viewer to analyze a RAT infection on port 8080.

### PowerShell Detection
Use `Get-WinEvent` to filter for known malicious destination ports:
```powershell
Get-WinEvent -Path <Path to Log> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=<Port>'
```
- Helps detect communication between infected hosts and C2 servers.

---

# Task 8: Persistence Techniques

## Overview
Attackers use persistence techniques to maintain access after initial compromise. This task focuses on startup script modifications and registry modifications for persistence.

## Detection Methods

### Hunting Startup Persistence
- Monitor for files created in `C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`.
- **Viewing Attack Logs:** Open `T1023.evtx` in Event Viewer to analyze a `persist.exe` file dropped into the Startup folder.

### Hunting Registry Key Persistence
- Detect modifications to registry keys under:
```mathematica
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```
- **Viewing Attack Logs:** Open `T1060.evtx` to identify a malicious registry entry pointing to `malicious.exe` in `C:\Windows\System32\`.

### Filtering with PowerShell
Use event filtering to identify registry changes for persistence:
```powershell
Get-WinEvent -Path <Path to Log> -FilterXPath '*/System/EventID=13'
```
- Focuses on registry modifications relevant to persistence mechanisms.

---

# Task 9: Detecting Evasion Techniques

## Overview
Attackers use evasion techniques like Alternate Data Streams (ADS) and Process Injection to bypass detection. This task focuses on identifying hidden files and injected remote threads.

## Detection Methods

### Hunting Alternate Data Streams (ADS)
- **Event ID 15 (Sysmon):** Detects files created using ADS in Temp and Startup folders.
- **Viewing Attack Logs:** Open `Hunting_ADS.evtx` to analyze hidden files using alternate data streams.

### Detecting Process Injection (Remote Threads)
- **Event ID 8 (Sysmon):** Detects creation of remote threads (e.g., DLL Injection, Process Hollowing).
- **Viewing Attack Logs:** Open `Detecting_RemoteThreads.evtx` to examine a PowerShell script injecting code into `notepad.exe` using Reflective PE Injection.

### PowerShell Detection
Use `Get-WinEvent` to identify remote thread creation:
```powershell
Get-WinEvent -Path <Path to Log> -FilterXPath '*/System/EventID=8'
```
- Helps pinpoint malicious injections into legitimate processes.

---

# Task 10: Practical Investigations

## Overview
Perform hands-on investigations using real-world event logs.

## Investigations

### Investigation 1 – Malicious USB Drop
- Examine `Investigation-1.evtx` to trace the origin and execution of the malicious file introduced via USB.

### Investigation 2 – HTML File Execution
- Analyze `Investigation-2.evtx` to identify how a malicious script masquerading as an HTML file executed on the system.

### Investigation 3 – Unauthorized Access Attempts
- Examine `Investigation-3.evtx` for suspicious access patterns that indicate unauthorized entry attempts.

---

# Key Takeaways
- **Mimikatz detection** relies on monitoring LSASS behavior and filtering non-suspicious processes.
- **RAT detection** involves identifying suspicious ports used for remote control.
- **Persistence detection** focuses on file creation in startup locations and registry modifications.
- **Evasion techniques** like ADS and process injections require granular logging and event analysis.
- **Practical investigations** help correlate event data to real-world attack scenarios.
