# Event Logs in Windows

## Summary

### Event Logs Purpose:
- Record system events for auditing, troubleshooting, and security analysis.
- Used by system administrators, IT technicians, and security teams.
- SIEMs like Splunk and Elastic help correlate logs from multiple sources.

### Windows Event Logs:
- Stored in binary format (.evt/.evtx) at `C:\Windows\System32\winevt\Logs`.
- Not viewable in text editors; can be converted to XML via Windows API.

### Types of Event Logs:
- **System Logs** – OS-related events.
- **Security Logs** – Login/logout and security-related activities.
- **Application Logs** – Application-related events.
- **Directory Service Events** – Active Directory changes.
- **File Replication Service Events** – Windows Server group policy sharing.
- **DNS Event Logs** – Domain-related logs.
- **Custom Logs** – App-specific logs.

### Event Log Types (from Microsoft Docs):
- Information, Warning, Error, Success Audit, Failure Audit.

### Accessing Windows Event Logs:
- **Event Viewer (GUI)** – Microsoft MMC snap-in.
- **Wevtutil.exe (CLI)** – Command-line tool for querying, exporting, and clearing logs.
- **Get-WinEvent (PowerShell Cmdlet)** – Queries logs locally and remotely.

### Event Viewer Overview:
- Three panes: Log providers (left), Event details (middle), Actions (right).
- Supports log filtering, custom views, and remote log access.
- Logs can be rotated or cleared, which can be exploited by attackers.

### Wevtutil.exe Tool:
- Retrieves event logs and publisher info.
- Supports querying, exporting, and clearing logs.
- Can run commands remotely.

### Get-WinEvent Cmdlet (PowerShell):
- Replaces `Get-EventLog`.
- Retrieves logs and event providers.
- Allows filtering using XPath, XML, and hash tables.

---

## Summary of Log Filtering and Event Monitoring in Windows

### Log Filtering with PowerShell

Use `Get-WinEvent` and `Where-Object` to filter logs by provider name:

```powershell
Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }
```

For efficiency, use the `-FilterHashtable` parameter instead of `Where-Object`:

```powershell
Get-WinEvent -FilterHashtable @{ LogName='Application'; ProviderName='WLMS' }
```

Hash table syntax:

```powershell
@{ <name> = <value>; [<name> = <value> ] ...}
```

### Filtering with XPath

XPath allows advanced event filtering using XML queries.

Example query to filter logs with severity level ≤ 3 in the last 24 hours:

```powershell
*[System[(Level <= 3) and TimeCreated[timediff(@SystemTime) <= 86400000]]]
```

Example PowerShell command:

```powershell
Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'
```

To filter by Provider Name:

```powershell
Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"]'
```

Combine multiple filters:

```powershell
Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'
```

Querying for `TargetUserName` in security logs:

```powershell
Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System"' -MaxEvents 1
```

### Event ID Monitoring

Important event IDs:
- **7045 (System Log)** → New service installed.
- **2006/2033** → Firewall rule deleted.
- **4688** → Process creation (requires command-line auditing enabled).

### Resources for Event Monitoring
- **Windows Logging Cheat Sheet** – Covers key event IDs.
- **NSA’s "Spotting the Adversary with Windows Event Log Monitoring"** – Guides threat detection.
- **MITRE ATT&CK Framework** – Helps in tracking attack techniques.
- **Microsoft Security Audit Guides** – Best practices for monitoring Active Directory.

### Enabling PowerShell & Process Logging

**PowerShell Logging (Enable via Group Policy/Registry)**

Path: `Local Computer Policy > Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell`

**Audit Process Creation (Generates Event ID 4688)**

Path: `Local Computer Policy > Computer Configuration > Administrative Templates > System > Audit Process Creation`
