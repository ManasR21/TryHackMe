# General Points
- TShark is the CLI version of Wireshark, sharing display filters and many features.
- Options apply to all packets unless a display filter is specified.
- TShark explains parameters at the beginning of the output.

# Key Features & Commands

## Colorized Output
- Helps in quick analysis by highlighting packets.
- **Command:**
  ```sh
  tshark --color
  ```

## Statistics (-z parameter)
- Provides various statistics for packet analysis.
- **View available options:**
  ```sh
  tshark -z help
  ```

## Protocol Hierarchy (-z io,phs -q)
- Displays protocols, frame numbers, and packet sizes in a tree view.
- **Command:**
  ```sh
  tshark -r file.pcapng -z io,phs -q
  ```
- **Filter for specific protocols:**
  ```sh
  tshark -r file.pcapng -z io,phs,udp -q
  ```

## Packet Lengths Tree (-z plen,tree -q)
- Shows packet size distribution for anomaly detection.
- **Command:**
  ```sh
  tshark -r file.pcapng -z plen,tree -q
  ```

## Endpoints (-z endpoints,ip -q)
- Lists unique endpoints and associated packet counts.
- **Command:**
  ```sh
  tshark -r file.pcapng -z endpoints,ip -q
  ```
- **Supports filtering by:** eth, ip, ipv6, tcp, udp, wlan.

## Conversations (-z conv,ip -q)
- Displays traffic flow between two connection points.
- **Command:**
  ```sh
  tshark -r file.pcapng -z conv,ip -q
  ```

## Expert Info (-z expert -q)
- Shows automatic comments and alerts from Wireshark.
- **Command:**
  ```sh
  tshark -r file.pcapng -z expert -q
  ```




# TShark Filtering Options & Statistics

## 1. General Filtering Options:
- Filters exist for multiple protocols.
- Command-line filters mirror GUI-based Wireshark features.

## 2. IPv4 & IPv6 Statistics:
- `-z ptype,tree -q`: Displays protocol distribution.
- `-z ip_hosts,tree -q`: Lists all IPs in the capture.
- `-z ip_srcdst,tree -q`: Shows source and destination addresses.
- `-z dests,tree -q`: Filters outgoing traffic and associated ports.

## 3. DNS Statistics:
- `-z dns,tree -q`: Summarizes DNS traffic, including queries and responses.

## 4. HTTP Statistics:
- `-z http,tree -q`: Displays HTTP request/response statistics.
- `-z http2,tree -q`: Similar but for HTTP/2.
- `-z http_srv,tree -q`: Shows load distribution.
- `-z http_req,tree -q`: Lists HTTP requests.
- `-z http_seq,tree -q`: Correlates requests and responses.





# Follow Stream

## Allows tracking of TCP, UDP, HTTP, and HTTP2 streams.

### Syntax:
```
-z follow,<protocol>,ascii,<stream_number> -q
```

### Example:
- **TCP Stream:**
  ```
  tshark -z follow,tcp,ascii,0 -q
  ```
- **UDP Stream:**
  ```
  tshark -z follow,udp,ascii,0 -q
  ```
- **HTTP Stream:**
  ```
  tshark -z follow,http,ascii,0 -q
  ```

---

# Export Objects

## Extracts files from captured traffic (DICOM, HTTP, IMF, SMB, TFTP).

### Syntax:
```
--export-objects <protocol>,<target_folder> -q
```

### Example:
- **Extract HTTP objects:**
  ```bash
  tshark -r demo.pcapng --export-objects http,/home/ubuntu/Desktop/extracted-by-tshark -q
  ```

---

# Credentials Extraction

## Detects cleartext credentials from FTP, HTTP, IMAP, POP, and SMTP.

### Syntax:
```
-z credentials -q
```

### Example:
- **Extract credentials from a pcap file:**
  ```bash
  tshark -r credentials.pcap -z credentials -q
  ```

### Output:
Displays usernames and related packet numbers for analysis.






# Advanced Filtering Options in TShark

## 1. Filtering Operators:

### Contains:
- Searches for a value inside packets (case-sensitive).
- Example: 
  ```bash
  http.server contains "Apache"
  ```

### Matches:
- Searches using regex (case-insensitive, may have a margin of error).
- Example:
  ```bash
  http.request.method matches "(GET|POST)"
  ```

## 2. Extract Fields:
- Helps extract specific data fields from packets for better analysis.
- Syntax:
  ```bash
  tshark -r demo.pcapng -T fields -e ip.src -e ip.dst -E header=y
  ```
- Example output:
  ```
  ip.src              ip.dst  
  145.254.160.237     65.208.228.223  
  ```

These advanced filtering options help in targeted packet analysis and data extraction.






# Use Cases for Security Analysts in TShark

## 1. Extracting Hostnames
- Extracts DHCP hostnames from pcap files.
- Handles duplicate values using Linux utilities:
  ```bash
  tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname | awk NF | sort -r | uniq -c | sort -r
  ```
- Outputs hostnames sorted by frequency.

## 2. Extracting DNS Queries
- Identifies queried domains from pcap files.
- Uses sorting and counting to prioritize results:
  ```bash
  tshark -r dns-queries.pcap -T fields -e dns.qry.name | awk NF | sort -r | uniq -c | sort -r
  ```
- Helps detect suspicious domain activity.

## 3. Extracting User Agents
- Retrieves user agents from HTTP traffic.
- Useful for identifying unusual or malicious requests:
  ```bash
  tshark -r user-agents.pcap -T fields -e http.user_agent | awk NF | sort -r | uniq -c | sort -r
  ```
- Helps in fingerprinting browsers and tools (e.g., Nmap, sqlmap).

These techniques assist in forensic analysis, threat hunting, and anomaly detection.

