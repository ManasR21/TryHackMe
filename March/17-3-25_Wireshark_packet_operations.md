## **Wireshark Packet Operations :  Summary**

---

### **Task 2: Statistics | Summary**
- **Statistics Menu**: Provides detailed insights into traffic, protocol usage, endpoints, and conversations within a capture file.
- **Resolved Addresses**: Displays a list of resolved IPs and hostnames, primarily obtained from DNS responses.
- **Protocol Hierarchy**: Presents a hierarchical view of all protocols identified in the capture, with details on packet counts, percentages, and byte sizes.
- **Conversations**: Summarizes traffic details between two communicating endpoints across Ethernet, IPv4, IPv6, TCP, and UDP.
- **Endpoints**: Lists unique communication endpoints (like MAC addresses, IP addresses, TCP/UDP ports) with statistics like packet count and bytes.
- **Name Resolution**: Converts numeric addresses to readable names for MAC, IP, and ports. Enable this via **Edit → Preferences → Name Resolution**.
- **GeoIP**: Maps IP addresses to geographic locations. Requires setting up a MaxMind GeoIP database.

---

### **Task 3: Statistics | Protocol Details**
- **IPv4 & IPv6 Stats**: Provides detailed statistics based on specific IP versions, including traffic patterns and protocol breakdowns.
- **DNS Stats**: Shows detailed information about DNS queries and responses, such as query types and response codes.
- **HTTP Stats**: Displays statistics for HTTP traffic, including methods (GET, POST), response codes, and original request URIs.

---

### **Task 4: Packet Filtering | Principles**
- **Capture Filters**:
  - Applied during the data capture process.
  - Based on protocols, ports, and hosts (e.g., `tcp port 80`).
- **Display Filters**:
  - Used post-capture to refine analysis.
  - Supports filtering across 3000+ protocols.
- **Filter Syntax**: Utilizes comparison (`==`, `!=`), logical (`and`, `or`, `not`), and relational (`>`, `<`) operators.
- **Name Resolution**: Facilitates easy understanding of packet details by resolving names.
- **Display Filter Expression**: Provides an interactive interface to build complex filters using predefined protocol fields.
- **Coloring Rules**: Helps visualize filtered packets with specific color codes for clarity.

---

### **Task 5: Packet Filtering | Protocol Filters**
- **IP Filters**:
  - Filter based on network-layer attributes like source/destination IP, TTL (e.g., `ip.src == 192.168.1.1`).
- **TCP Filters**:
  - Focus on transport-layer fields like port numbers, sequence numbers, flags (e.g., `tcp.port == 80`, `tcp.flags.syn == 1`).
- **UDP Filters**:
  - Filter using UDP-specific attributes (e.g., `udp.port == 53` for DNS traffic).
- **Application Protocol Filters**:
  - Filter packets for specific protocols like HTTP or DNS (e.g., `http.request.method == "GET"`, `dns.qry.type == 1`).
- **Filter Examples**:
  - Filter packets with TTL greater than 50: `ip.ttl > 50`.
  - Capture only DNS traffic: `udp.port == 53`.
  - Highlight TCP SYN packets: `tcp.flags.syn == 1 and tcp.flags.ack == 0`.

---

### **Task 6: Advanced Filtering**
- **Advanced Operators**:
  - `contains`: Filter packets containing specific substrings (e.g., `http.request.uri contains "login"`).
  - `matches`: Use regex for advanced pattern matching (e.g., `http.host matches "^www\\..*\\.com$"`).
  - `in`: Specify a set for filtering (e.g., `ip.addr in {192.168.1.1 192.168.1.2}`).
  - `upper/lower`: Perform case-insensitive filtering (e.g., `upper(http.host) contains "EXAMPLE"`).
- **Bookmarks & Filter Buttons**: Allows saving frequently used filters for quick access during analysis.
- **Profiles**: Enables the creation of custom configurations for recurring investigative scenarios. Profiles can store specific filters, color settings, and layout preferences.

---
