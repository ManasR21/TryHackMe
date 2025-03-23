# TShark Traffic Analysis - Case: Directory Curiosity

## **Introduction**
- Investigate traffic data as part of a SOC team.
- Use TShark to analyze captured traffic.

## **Case: Directory Curiosity!**
### **Alert Triggered**
- "A user came across a poor file index, and their curiosity led to problems."
- Investigate **directory-curiosity.pcap** located in `~/Desktop/exercise-files`.
- Tools: **TShark, VirusTotal**.

### **Investigation Findings**
#### **DNS Queries & VirusTotal Analysis**
- **Malicious/Suspicious Domain**: `jx2-bavuong[.]com`
- **Total HTTP Requests to Malicious Domain**: `14`
- **Associated IP Address**: `141[.]164[.]41[.]174`
- **Server Info**: `Apache/2.2.11 (Win32) DAV/2 mod_ssl/2.2.11 OpenSSL/0.9.8i PHP/5.2.9`

#### **TCP Stream Analysis**
- **Number of Listed Files**: `3`
- **First Filename**: `123[.]php`

#### **Exporting HTTP Traffic Objects**
- Command:
  ```sh
  tshark -r directory-curiosity.pcap --export-objects http,/home/ubuntu/Desktop/exercise-files -q
  ```
  - `-r directory-curiosity.pcap`: Reads the capture file.
  - `--export-objects http,/home/ubuntu/Desktop/exercise-files`: Extracts and saves HTTP objects.
  - `-q`: Runs quietly, suppressing packet summary output.

- **Downloaded Executable File**: `vlauto[.]exe`
- **SHA256 Value**:
  ```sh
  sha256 file_name
  ```
  **SHA256 Hash**: `b4851333efaf399889456f78eac0fd532e9d8791b23a86a19402c1164aed20de`

#### **VirusTotal Analysis**
- **PEiD Packer**: `.NET executable`
- **Lastline Sandbox Classification**: `MALWARE TROJAN`

## **Conclusion**
The investigation confirms a **true positive alert** due to malicious activity involving **file indexing vulnerabilities** and the download of a **malicious executable**.

