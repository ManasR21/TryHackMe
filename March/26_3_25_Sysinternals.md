# Sysinternals Tools Compilation

## Task 1. Introduction
### What are the tools known as Sysinternals?
The Sysinternals tools is a compilation of over 70+ Windows-based tools. Each of the tools falls into one of the following categories:
- File and Disk Utilities
- Networking Utilities
- Process Utilities
- Security Utilities
- System Information
- Miscellaneous

The Sysinternals tools and its website (sysinternals.com) were created by Mark Russinovich back in the late ’90s, along with Bryce Cogswell under the company Wininternals Software. In 2005, Microsoft acquired Wininternals Software, and Mark Russinovich joined Microsoft. Today, he is the CTO of Microsoft Azure.

**Question 1. When did Microsoft acquire the Sysinternals tools?**
**Answer: 2005**

---
## Task 2. Install the Sysinternals Suite
The Sysinternals tool(s) can be downloaded and run from the local system, or the tool(s) can be run from the web.

If you wish to download a tool or two but not the entire suite, navigate to the Sysinternals Utilities Index page: [Sysinternals Downloads](https://docs.microsoft.com/en-us/sysinternals/downloads/). If you wish to download the Sysinternals Suite, you can download the zip file from this page.

### Setting up the Environment Variables
- Open **System Properties** by running `sysdm.cpl`
- Click on the **Advanced** tab
- Select **Path** under System Variables and select **Edit…** then OK.
- In the next screen, select **New** and enter the folder path where the Sysinternals Suite was extracted.

To confirm the setup, open a new command prompt (elevated) and run the tools from any location.

Alternatively, use PowerShell to install:
```
Download-SysInternalsTools C:\Tools\Sysint
```

**Question 2. What is the last tool listed within the Sysinternals Suite?**
**Answer: ZoomIt**

---
## Task 3. Using Sysinternals Live
Sysinternals Live allows running tools directly from the web using paths like:
```
\live.sysinternals.com\tools\<toolname>
```
Before using it, ensure:
- **WebDAV Client** is installed and running (`services.msc` → WebClient)
- **Network Discovery** is enabled

**Methods to run tools:**
1. Run directly from the command line:
   ```
   \live.sysinternals.com\tools\procmon.exe
   ```
2. Map a network drive:
   ```
   net use * \\live.sysinternals.com\tools
   ```

**Question 3. What service needs to be enabled on the local host to interact with live.sysinternals.com?**
**Answer: WebClient**

---
## Task 4. File and Disk Utilities
### Streams (Alternate Data Streams - ADS)
Windows NTFS allows data to be hidden within files using ADS. To inspect ADS:
```
dir /r
```
**Question 4. What is the text within the ADS for file.txt?**
**Answer: I am hiding in the stream.**

**WHOIS Tool:**
Find the ISP for an IP address using:
```
whois 52.154.170.73
```
**Answer: Microsoft Corporation**

---
## Task 5. Process Utilities
Using **Autoruns**, check the `Image Hijacks` tab for new entries.

**Question 1. What entry was updated?**
**Answer: taskmgr.exe**

**Question 2. What is the updated value?**
Modify the debugger entry in Autoruns.
**Answer: C:\TOOLS\SYSINT\PROCEXP.EXE**

To analyze binary files, use the **Strings** tool:
```
strings ZoomIt.exe
```
**Question 3. What is the full path to the .pdb file in ZoomIt.exe?**
**Answer: C:\agent\_work\112\s\Win32\Release\ZoomIt.pdb**

---


## Task 6: Sysinternals Process Utilities

### Autoruns

**Official Definition:**
"This utility, which has the most comprehensive knowledge of auto-starting locations of any startup monitor, shows you what programs are configured to run during system bootup or login, and when you start various built-in Windows applications like Internet Explorer, Explorer and media players. These programs and drivers include ones in your startup folder, Run, RunOnce, and other Registry keys. Autoruns reports Explorer shell extensions, toolbars, browser helper objects, Winlogon notifications, auto-start services, and much more. Autoruns goes way beyond other autostart utilities."

**Usage:**
- This tool helps in identifying malicious entries created on a local machine for persistence.
- Launch Autoruns and analyze the entries in the "Everything" tab.
- Check different tabs to inspect auto-start entries.

### ProcDump

**Official Definition:**
"ProcDump is a command-line utility whose primary purpose is monitoring an application for CPU spikes and generating crash dumps during a spike that an administrator or developer can use to determine the cause of the spike."

**Usage:**
- Use it to capture minidumps or full dumps of processes.
- Alternative: Use Process Explorer to create a dump by right-clicking a process and selecting "Create Dump."

### Process Explorer

**Official Definition:**
"The Process Explorer display consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode you'll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you'll see the DLLs and memory-mapped files that the process has loaded."

**Usage:**
- Monitor active processes and analyze their associated services, DLLs, and TCP/IP connections.
- Verify process signatures and replace Task Manager if needed.
- Investigate suspicious processes by analyzing their properties.

### Process Monitor (ProcMon)

**Official Definition:**
"Process Monitor is an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity. It combines the features of two legacy Sysinternals utilities, Filemon and Regmon, and adds an extensive list of enhancements."

**Usage:**
- Capture real-time system activity, including file system operations and registry changes.
- Use filters to isolate relevant events and minimize data overload.
- Analyze captured events to identify suspicious or malicious activity.

### PsExec

**Official Definition:**
"PsExec is a lightweight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software."

**Usage:**
- Execute commands on remote systems.
- Commonly used for lateral movement by adversaries.
- Associated MITRE ATT&CK techniques: T1570, T1021.002, T1569.002.

### Additional Resources:
- [Sysinternals Process Utilities](https://docs.microsoft.com/en-us/sysinternals/downloads/process-utilities)
- [Talos Reputation Center](https://talosintelligence.com/reputation_center/lookup)


## Task 7

## Sysmon

**System Monitor (Sysmon)** is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time. By collecting the events it generates using Windows Event Collection or SIEM agents and subsequently analyzing them, you can identify malicious or anomalous activity and understand how intruders and malware operate on your network.

**Link:** [Sysinternals Security Utilities](https://docs.microsoft.com/en-us/sysinternals/downloads/security-utilities)


