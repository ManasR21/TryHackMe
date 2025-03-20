## **Command-Line Packet Analysis Hints (TShark)**  

### **1. Overview**  
- TShark is a command-line network packet analysis tool.  
- Ideal for automation, deep packet analysis, and integration with scripts.  

### **2. Common CLI Utilities for Packet Analysis**  
- **capinfos** – Summarizes capture file details.  
- **grep** – Searches plain-text data.  
- **cut** – Extracts parts of lines from data sources.  
- **uniq** – Removes duplicate lines.  
- **nl** – Numbers displayed lines.  
- **sed** – Stream editor for modifying text.  
- **awk** – Pattern searching and text processing.  

### **3. TShark CLI Parameters**  

| Parameter | Purpose | Example |
|-----------|---------|---------|
| `-h` | Help page | `tshark -h` |
| `-v` | Version info | `tshark -v` |
| `-D` | List interfaces | `tshark -D` |
| `-i` | Select interface | `tshark -i 1` |
| `-r` | Read pcap file | `tshark -r file.pcap` |
| `-c` | Limit packet count | `tshark -c 10` |
| `-w` | Write packets to file | `tshark -w output.pcap` |
| `-V` | Verbose packet details | `tshark -V` |
| `-q` | Silent mode | `tshark -q` |
| `-x` | Hex and ASCII dump | `tshark -x` |

### **4. Capture Conditions (Autostop & Looping)**  
- **`-a` (Autostop)**: Stop capturing based on time, file size, or number of files.  
  - `tshark -w test.pcap -a duration:10` (Stop after 10s)  
- **`-b` (Ring Buffer)**: Creates multiple capture files in a loop.  
  - `tshark -w test.pcap -b filesize:10` (New file after 10KB)  

### **5. Packet Filtering**  
- **Capture Filters (`-f`)** – Applied before capturing traffic.  
- **Display Filters (`-Y`)** – Applied to analyze captured packets.  

#### **Capture Filters Examples:**  

| Type | Command |  
|------|---------|  
| Host filtering | `tshark -f "host 10.10.10.10"` |  
| Network range | `tshark -f "net 192.168.1.0/24"` |  
| Port filtering | `tshark -f "port 80"` |  
| Protocol filtering | `tshark -f "tcp"` |  

#### **Display Filters Examples:**  

| Type | Command |  
|------|---------|  
| IP filtering | `tshark -Y "ip.addr == 10.10.10.10"` |  
| TCP port filtering | `tshark -Y "tcp.port == 443"` |  
| HTTP packets | `tshark -Y "http"` |  
| DNS filtering | `tshark -Y "dns"` |  

### **6. Notes & Best Practices**  
- Use capture filters to minimize packet overload.  
- Display filters help refine analysis post-capture.  
- Combine `-a` and `-b` parameters to control capture size and duration.  
- Requires superuser privileges (`sudo`) for live traffic sniffing.
