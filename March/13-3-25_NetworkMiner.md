# NetworkMiner Overview

- NetworkMiner is an open-source Network Forensic Analysis Tool (NFAT) for Windows, also compatible with Linux, Mac OS X, and FreeBSD.
- Functions as a passive network sniffer/packet capturing tool to detect OS, sessions, hostnames, open ports, etc., without generating network traffic.
- Can parse PCAP files for offline analysis and reassemble transmitted files and certificates.
- Popular among incident response teams and law enforcement since its first release in 2007.
- Used by companies and organizations worldwide.

## Goal of Network Forensics
- Detect malicious activities, security breaches, and anomalies using network traffic analysis.

## Role of NetworkMiner
- Provides quick and useful insights for starting forensic investigations.
- Captures host context like IP, MAC, hostnames, and OS information.
- Identifies potential attack indicators, such as traffic spikes or port scans.
- Detects tools or toolkits used in attacks, e.g., Nmap.

## Supported Data Types in Network Forensics
- **Live Traffic**
- **Traffic Captures** (e.g., PCAP files)
- **Log Files**

## NetworkMiner's Capabilities
- Processes both PCAP files and live traffic.
- Focus is on analyzing live and captured traffic.

## NetworkMiner in a Nutshell

### Key Capabilities
| Capability                | Description                                                        |
|---------------------------|--------------------------------------------------------------------|
| Traffic Sniffing          | Intercepts and logs packets passing through the network.            |
| Parsing PCAP Files        | Parses PCAP files and displays detailed packet content.             |
| Protocol Analysis         | Identifies protocols used in the parsed PCAP file.                  |
| OS Fingerprinting         | Detects OS using tools like Satori and p0f from the PCAP file.      |
| File Extraction           | Extracts images, HTML files, and emails from PCAP files.            |
| Credential Grabbing       | Extracts credentials from the parsed PCAP file.                     |
| Clear Text Keyword Parsing| Extracts cleartext keywords and strings from the PCAP file.          |

> **Edition:** Using the Free Edition in this context. The Professional Edition offers more features.

### Operating Modes
- **Sniffer Mode**
  - Available only on Windows.
  - Not as reliable as dedicated sniffers like Wireshark or tcpdump.
  - Best used for basic sniffing, but not recommended for primary sniffing tasks.

- **Packet Parsing/Processing Mode**
  - Parses traffic captures (PCAPs) for a quick overview.
  - Ideal for grabbing the "low-hanging fruit" before deeper investigations.

### Pros and Cons

✅ **Pros**:
- Effective OS fingerprinting.
- Easy and quick file extraction.
- Capable of credential grabbing.
- Supports cleartext keyword parsing.
- Provides an overall quick overview of captured data.

❌ **Cons**:
- Not reliable for active sniffing.
- Inefficient for analyzing large PCAP files.
- Limited filtering options.
- Not designed for manual traffic investigations.

### Differences Between NetworkMiner and Wireshark
- **NetworkMiner**: Great for quick overviews and basic analysis.
- **Wireshark**: Ideal for deep, detailed investigations.

**Best Practice:**
1. Record network traffic.
2. Use NetworkMiner for an initial overview.
3. Dive deeper with Wireshark for thorough analysis.

---

# NetworkMiner Features

## Landing Page
This is the landing page of the NetworkMiner. Once you open the application, this screen loads up.

## File Menu
- Load a PCAP file or receive PCAP over IP.
- Drag and drop PCAP files for ease.
- NetworkMiner can receive PCAPs over IP but this feature is skipped in the current context.

## Tools Menu
- Clear the dashboard and remove captured data.

## Help Menu
- Provides information on updates and the current version.

## Case Panel
- Displays the list of investigated PCAP files.
- Options to reload/refresh, view metadata, and remove files.

## Hosts Menu
- Shows identified hosts with details such as:
  - IP Address
  - MAC Address
  - OS Type
  - Open Ports
  - Sent/Received Packets
  - Session Details
- OS fingerprinting uses Satori and p0f, while MAC addresses use mac-ages GitHub repo.
- Allows sorting and color customization.
- Some features (like OSINT lookup) are premium-only.

## Sessions Menu
- Displays detected sessions with details such as:
  - Frame Number
  - Client and Server Address
  - Ports and Protocols
  - Start Time
- Allows filtering by keywords and supports inputs like "ExactPhrase", "AllWords", "AnyWord", and "RegExe".

## DNS Menu
- Displays DNS queries with details like:
  - Frame Number, Timestamp, Client/Server, Ports, DNS Time, and more.
- Features like Alexa Top 1M are premium-only.

## Credentials Menu
- Extracts credentials from investigated PCAPs:
  - Kerberos, NTLM, HTTP cookies, IMAP, FTP, SMTP, etc.
- Compatible with Hashcat and John the Ripper for decryption.
- Right-click options for copying credentials easily.

## Files Menu
- Displays extracted files with details such as:
  - Frame Number, Filename, Extension, Size, Source/Destination Address, Ports, Protocol, and Timestamp.
- Some features like OSINT hash lookup are premium-only.

## Images Menu
- Displays extracted images with options to open, zoom, and view details on hover.

## Parameters Menu
- Displays extracted parameters with details like:
  - Parameter Name/Value, Frame Number, Source/Destination Host and Port, and Timestamp.

## Keywords Menu
- Displays extracted keywords with filtering options.
- Requires reloading case files after updating search keywords.

## Messages Menu
- Displays extracted emails, chats, and messages with details like:
  - Frame Number, Sender/Receiver, Protocol, Timestamp, and Attachments.

## Anomalies Menu
- Detects anomalies like EternalBlue exploit attempts and spoofing.

---

# Version Differences

## Significant Changes between Versions 1.6 and 2.7

1. **MAC Address Processing**
   - Available after version 2.
   - Identifies MAC address conflicts.

2. **Packet Details Processing**
   - More detailed packet handling in version 1.6.

3. **Frame Processing**
   - Detailed frame analysis in version 1.6.

4. **Parameter Processing**
   - More extensive parameter handling in version 2 and above.

5. **Cleartext Data Processing**
   - Version 1.6 provides a dedicated tab for cleartext data.
