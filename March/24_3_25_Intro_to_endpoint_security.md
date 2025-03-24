## Core Windows Processes
- Understanding Windows OS fundamentals is essential for log analysis.
- Task Manager is a built-in tool to monitor system processes and resource usage.
- Core Windows Processes:
  - `System`
  - `System > smss.exe`
  - `csrss.exe`
  - `wininit.exe`
  - `wininit.exe > services.exe`
  - `wininit.exe > services.exe > svchost.exe`
  - `lsass.exe`
  - `winlogon.exe`
  - `explorer.exe`
- Parent-child relationships are crucial for identifying normal process behavior.

## Sysinternals Tools
- A set of 70+ tools for Windows analysis.
- Categories:
  - File and Disk Utilities
  - Networking Utilities
  - Process Utilities
  - Security Utilities
  - System Information
  - Miscellaneous
- Important tools:
  - **TCPView**: Monitors TCP/UDP connections and process ownership.
  - **Process Explorer**: Provides detailed process analysis including services, network traffic, and DLLs.

## Windows Event Logs
- Stored in binary format (`.evt`, `.evtx`) at `C:\Windows\System32\winevt\Logs`.
- Access methods:
  - **Event Viewer** (GUI)
  - **Wevtutil.exe** (CLI)
  - **Get-WinEvent** (PowerShell)

## Sysmon
- Monitors and logs detailed system events.
- Used with SIEM systems for anomaly detection.
- Provides 27 Event IDs for granular logging.

## OSQuery
- Open-source tool for querying endpoint data using SQL syntax.
- Supports multiple platforms: Windows, Linux, macOS, FreeBSD.
- Example command:
  ```sql
  select pid, name, path from processes where name='lsass.exe';
  ```
- **Kolide Fleet**: Enables querying multiple endpoints remotely.

## Wazuh
- Open-source EDR solution for security monitoring.
- Uses a management-agent model for endpoint monitoring.
- Capabilities:
  - Vulnerability assessment
  - Suspicious activity monitoring
  - Data visualization
  - Behavioral analysis

## Event Correlation
- Connects related artifacts across multiple log sources.
- Example:
  - Sysmon logs (Event ID 3: Network Connection) vs Firewall Logs.
  - Provides insights into:
    - Source & Destination IPs
    - Ports & Protocols
    - Process names & User accounts

## Baselining
- Establishes normal behavior for endpoint security monitoring.
- Identifies deviations indicating potential threats.
- Example:
  - **Baseline**: Employees work in London from 9 AM - 6 PM.
  - **Unusual Activity**: A VPN login from Singapore at 3 AM.
  - Helps distinguish expected vs suspicious activities.

