# Anomalous DNS, Phishing, and Log4J Investigation Summary

## **Task 2: Anomalous DNS**

- **Inspecting DNS Records for IPv6 (AAAA)**  
  This command processes the DNS log to count how many DNS queries were made for each record type, such as A (IPv4), AAAA (IPv6), etc. This helps in identifying the presence and volume of IPv6 queries, which could indicate unusual network behavior if unexpected.
  ```bash
  cat dns.log | zeek-cut qtype_name | sort | uniq -c
  ```
  - `cat dns.log`: Outputs the contents of the DNS log file.
  - `zeek-cut qtype_name`: Extracts the DNS query type (like A, AAAA, etc.).
  - `sort`: Sorts the extracted query types.
  - `uniq -c`: Counts and lists the number of occurrences for each unique query type.

- **Finding the Longest Connection Duration**  
  Identifies the longest-lasting network connection from the connection log, which can help detect persistent or suspicious connections that may be indicative of an attack or data exfiltration.
  ```bash
  cat conn.log | zeek-cut duration | sort -r | head -n 1
  ```
  - `cat conn.log`: Outputs the contents of the connection log file.
  - `zeek-cut duration`: Extracts the connection duration field.
  - `sort -r`: Sorts the durations in descending order.
  - `head -n 1`: Displays the longest (top) duration value.

- **Counting Unique Domain Queries**  
  Extracts and counts unique combinations of top-level and second-level domains, helping identify the diversity and frequency of external domains queried by the network.
  ```bash
  cat dns.log | zeek-cut query | awk -F '.' '{print $NF FS $(NF-1)}' | sort | uniq | wc -l
  ```
  - `cat dns.log`: Outputs the contents of the DNS log file.
  - `zeek-cut query`: Extracts the full domain queries.
  - `awk -F '.' '{print $NF FS $(NF-1)}'`: Splits domains by dots and prints the top-level and second-level domain parts.
  - `sort`: Sorts the domains.
  - `uniq`: Removes duplicate domain entries.
  - `wc -l`: Counts the number of unique domain entries.

- **Identifying Source Host IP Addresses**  
  Lists and counts the number of unique source IP addresses that initiated network connections, which can help in identifying potentially compromised or active hosts.
  ```bash
  cat conn.log | zeek-cut id.orig_h | sort | uniq -c
  ```
  - `cat conn.log`: Outputs the contents of the connection log file.
  - `zeek-cut id.orig_h`: Extracts the source IP address from each connection record.
  - `sort`: Sorts the IP addresses.
  - `uniq -c`: Counts and lists the unique IP addresses along with their frequency.

---

## **Task 3: Phishing**

- **Identifying Suspicious Source Address**  
  Similar to the DNS task, this command counts unique source IP addresses from the connection logs, which can help highlight any anomalous or suspicious originating IPs involved in potential phishing attempts.
  ```bash
  cat conn.log | zeek-cut id.orig_h | sort | uniq -c
  ```

- **Finding Malicious Domains from HTTP Logs**  
  Extracts the URI paths and associated hostnames from HTTP traffic to help identify potentially malicious domain activity.
  ```bash
  cat http.log | zeek-cut uri host
  ```
  - `cat http.log`: Outputs the contents of the HTTP log file.
  - `zeek-cut uri host`: Extracts the URI and host fields from HTTP requests.

- **Extracting File Hashes and MIME Types**  
  Extracts file hashes and MIME types from file analysis logs. This information is crucial for identifying potentially malicious files and their types for further analysis.
  ```bash
  cat files.log | zeek-cut mime_type md5
  ```
  - `cat files.log`: Outputs the contents of the file analysis log.
  - `zeek-cut mime_type md5`: Extracts the MIME type and MD5 hash of files observed.

- **Counting Queries for Specific Domains**  
  Aggregates and counts DNS queries based on the top-level and second-level domain names, helping to pinpoint which domains were frequently queried, which may be useful in detecting phishing-related domains.
  ```bash
  cat dns.log | zeek-cut query | awk -F '.' '{print $(NF-1)"."$NF}' | sort | uniq -c
  ```
  - `cat dns.log`: Outputs the DNS log contents.
  - `zeek-cut query`: Extracts the full domain queries.
  - `awk -F '.' '{print $(NF-1)"."$NF}'`: Extracts the second and top-level domains.
  - `sort`: Sorts the domains.
  - `uniq -c`: Counts and lists unique domain occurrences.

---

## **Task 4: Log4J**

- **Counting Signature Hits**  
  Counts the number of unique signature hits related to potential Log4J exploitation, helping quantify the extent of suspicious activities detected.
  ```bash
  cat signatures.log | zeek-cut sig_id | wc -l
  ```
  - `cat signatures.log`: Outputs the contents of the signatures log.
  - `zeek-cut sig_id`: Extracts signature IDs from the logs.
  - `wc -l`: Counts the total number of extracted signature IDs.

- **Identifying Tools from User-Agent Strings**  
  Analyzes the HTTP user-agent strings to identify the tools or software used in the HTTP requests, which can be helpful in detecting automated or malicious activity.
  ```bash
  cat http.log | zeek-cut user_agent | sort | uniq -c
  ```
  - `cat http.log`: Outputs the contents of the HTTP log file.
  - `zeek-cut user_agent`: Extracts the user-agent field.
  - `sort`: Sorts the user-agent strings.
  - `uniq -c`: Counts and lists unique user-agent occurrences.

- **Finding Exploit File Extensions**  
  Lists all unique URI paths from the HTTP log, which can be analyzed to detect potential file downloads related to exploits.
  ```bash
  cat http.log | zeek-cut uri | sort | uniq
  ```
  - `cat http.log`: Outputs the contents of the HTTP log file.
  - `zeek-cut uri`: Extracts the URI paths.
  - `sort | uniq`: Sorts and deduplicates the URIs.

- **Decoding Base64 Commands to Extract File Names**  
  Searches for Base64-encoded strings within the Log4J logs. These encoded strings could hide malicious payloads or commands that need to be analyzed.
  ```bash
  cat log4j.log | zeek-cut value | grep Base64
  ```
  - `cat log4j.log`: Outputs the contents of the Log4J-specific log.
  - `zeek-cut value`: Extracts the values field which could contain encoded strings.
  - `grep Base64`: Filters the output for lines containing "Base64", indicating encoded data.

---
