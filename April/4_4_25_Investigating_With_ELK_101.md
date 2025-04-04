# Elastic Stack Lab Summary

## 🔍 Learning Objectives
- Perform searches, apply filters, and save them
- Create visualizations in Kibana
- Investigate VPN logs for anomalies
- Build dashboards using saved elements

---

## 📦 Elastic Stack Overview
**Elastic Stack = Elasticsearch + Logstash + Beats + Kibana**

### 1. Elasticsearch
- Full-text search and analytics engine
- Stores JSON-formatted documents
- Supports RESTful API

### 2. Logstash
- Data processing engine
- Takes input from various sources, filters it, and outputs to destinations (like Elasticsearch or Kibana)
- Config file structure: `input`, `filter`, `output`

### 3. Beats
- Lightweight agents (data shippers) that send specific data to Elasticsearch
- Examples:
  - **Winlogbeat**: Windows event logs
  - **Packetbeat**: Network traffic flows

### 4. Kibana
- Web-based interface to visualize and analyze Elasticsearch data
- Supports dashboards, charts, tables, filters, etc.

---

## 🧭 Discover Tab (Kibana)
Used for exploring logs.

### Key Components:
- **Logs (Documents)**: Events with field-value pairs
- **Fields Pane**: List of normalized fields
- **Index Pattern**: Template for accessing structured data (e.g., `vpn_connections`)
- **Search Bar**: Write search queries using KQL (Kibana Query Language)
- **Time Filter**: Filter logs by time
- **Timeline**: View event spikes visually

### Filters and Tables:
- Use `+` to filter IN and `-` to filter OUT specific field values
- Create simplified tables from raw logs by selecting key fields

---

## 🔎 KQL (Kibana Query Language)
Supports both free-text and field-based search.

### 1. Free Text Search
- `"United States"`: Finds all documents with this exact term
- `United*`: Wildcard search for partial matches

### 2. Logical Operators
- `OR`: e.g., `"United States" OR "England"`
- `AND`: e.g., `"United States" AND "Virginia"`
- `NOT`: e.g., `"United States" AND NOT ("Florida")`

### 3. Field-Based Search
- Syntax: `field : value`
- Example: `Source_ip : 238.163.231.224 AND UserName : Suleman`

---

## 📊 Visualization Tab
Used to turn log data into visual formats:
- **Pie Charts, Tables, Bar Graphs**
- **Correlation**: Show relationships between fields (e.g., IPs vs. Source Country)

### Saving Visualizations
- Click Save > Add title/description > Add to existing or new dashboard

---

## 📋 Creating Custom Dashboards
Steps:
1. Go to Dashboard tab > Click *Create Dashboard*
2. Click *Add from Library*
3. Select saved searches/visualizations
4. Arrange components
5. Save the dashboard

---

## ✅ Final Notes
- Use saved searches and visualizations for quick insights
- Customize dashboards for log monitoring and threat analysis
- Explore more KQL syntax: [Kibana Query Language Guide](https://www.elastic.co/guide/en/kibana/7.17/kuery-query.html)

