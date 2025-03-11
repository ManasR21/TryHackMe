# Snort Challenge Tasks (Task 1 - 8)

## Task 1: Introduction
- Introduction to writing IDS rules and detecting various types of network traffic and vulnerabilities using Snort.

---

## Task 2: Writing IDS Rules (HTTP)
- Objective: Write Snort rules to detect HTTP traffic.
- Rule Example:
```snort
alert tcp any any -> any 80 (msg:"HTTP Traffic Detected"; sid:1000001; rev:1;)
```
- Tested with Snort and verified detection of HTTP traffic.

---

## Task 3: Writing IDS Rules (FTP)
- Objective: Write rules to detect FTP traffic and identify potential login attempts.
- Rule Example:
```snort
alert tcp any any -> any 21 (msg:"FTP Traffic Detected"; sid:1000002; rev:1;)
```
- Detected FTP traffic using the provided pcap files and Snort commands.

---

## Task 4: Writing IDS Rules (PNG)
- Objective: Detect PNG file transfers.
- Rule Example:
```snort
alert tcp any any -> any any (msg:"PNG File Detected"; content:"\x89PNG\x0D\x0A\x1A\x0A"; sid:1000003; rev:1;)
```
- Verified with Snort to ensure PNG file detection.

---

## Task 5: Writing IDS Rules (Torrent Metafile)
- Objective: Detect torrent metafiles in network traffic.
- Rule Example:
```snort
alert tcp any any -> any any (msg:"Torrent Metafile Detected"; content:"d8:announce"; sid:1000004; rev:1;)
```
- Successfully detected torrent-related traffic.

---

## Task 6: Troubleshooting Rule Syntax Errors
- **local-1.rules**: Fixed spacing error near "any".
```snort
alert tcp any 3372 -> any any (msg: "Troubleshooting 1"; sid:1000001; rev:1;)
```
- Detected packets: **16**.

- **local-2.rules**: Added missing port value.
```snort
alert icmp any any -> any any (msg: "Troubleshooting 2"; sid:1000001; rev:1;)
```
- Detected packets: **68**.

- **local-3.rules**: Resolved duplicate SID issue.
```snort
alert icmp any any -> any any (msg: "ICMP Packet Found"; sid:1000001; rev:1;)
alert tcp any any -> any 80,443 (msg: "HTTPX Packet Found"; sid:1000002; rev:1;)
```
- Detected packets: **87**.

- **local-4.rules**: Corrected "msg" syntax and duplicate SID.
```snort
alert icmp any any -> any any (msg: "ICMP Packet Found"; sid:1000001; rev:1;)
alert tcp any 80,443 -> any any (msg: "HTTPX Packet Found"; sid:1000002; rev:1;)
```
- Detected packets: **90**.

- **local-5.rules**: Replaced "<-" with "<>".
```snort
alert icmp any any <> any any (msg: "ICMP Packet Found"; sid:1000001; rev:1;)
alert icmp any any <> any any (msg: "Inbound ICMP Packet Found"; sid:1000002; rev:1;)
alert tcp any any -> any 80,443 (msg: "HTTPX Packet Found"; sid:1000003; rev:1;)
```
- Detected packets: **155**.

- **local-6.rules**: Added "nocase" to detect case-insensitive "GET" requests.
```snort
alert tcp any any <> any 80 (msg: "GET Request Found"; content:"|67 65 74|"; nocase; sid:100001; rev:1;)
```
- Detected packets: **2**.

- **local-7.rules**: Added a descriptive "msg".
```snort
alert tcp any any <> any 80 (msg:"html detected";content:"|2E 68 74 6D 6C|"; sid:100001; rev:1;)
```
- Required option: **msg**.

---

## Task 7: Using External Rules (MS17–010)
- Detected packets using provided rule:
```bash
sudo snort -A full -c local.rules -r ms-17-010.pcap
```
- Detected packets: **25154**.

- Custom rule to detect "\IPC$":
```snort
alert tcp any any -> any 445 (msg: "Exploit Detected!"; flow: to_server, established; content: "IPC$"; sid: 20244225; rev:3;)
```
- Detected packets: **12**.
- Requested Path: `\\192.168.116.138\IPC$`
- CVSS v2 Score: **9.3**.

---

## Task 8: Using External Rules (Log4j)
- Detected packets: **26**.
- Number of triggered rules: **4**.
- First six digits of triggered rule SIDs: **210037**.
- Custom rule to detect payload size between 770-855 bytes:
```snort
alert tcp any any -> any any (msg: "Packet payload size between 770 and 855 bytes detected"; dsize: 770<>855; sid: 1000001;)
```
- Detected packets: **41**.
- Encoding Algorithm: **Base64**.
- IP ID of corresponding packet: **62808**.
- CVSS v2 Score: **9.3**.

---


![Accomplished](March/11-3-25_Snort-Challenge-The-Basics/image.png)


