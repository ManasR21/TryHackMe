- Phishing Analysis Fundamentals
  
![image](https://github.com/user-attachments/assets/cc33a878-28c9-4164-9292-c53f85665717)
![image](https://github.com/user-attachments/assets/707e7b63-cc50-450a-80e9-9b2658b22b01)

- Phishing Emails in Action

![image](https://github.com/user-attachments/assets/96bd6c94-d1f2-45d9-b775-c5b35f6f0343)
![image](https://github.com/user-attachments/assets/b1b1f3b3-25ad-47e2-a7d5-23293fa74fbc)


- Phishing Analysis Tools

# Email Phishing Analysis Checklist and Tools

## 📧 Email Header Analysis

### Checklist:
- Sender email address
- Sender IP address
- Reverse lookup of sender IP
- Email subject line
- Recipient email address (To/CC/BCC)
- Reply-To address (if any)
- Date/Time

### Tools for Header Analysis:
- [Google Admin Toolbox Messageheader](https://toolbox.googleapps.com/apps/messageheader/analyzeheader)
- [Microsoft Message Header Analyzer](https://mha.azurewebsites.net/)
- [Mailheader.org](https://mailheader.org)

## 📬 Email Body and Attachment Analysis

### Checklist:
- URLs (including unshortened versions)
- Attachment name
- SHA256 or MD5 hash of attachments

⚠️ **Do not click on links or open attachments.**

### Tools for URL & Domain Analysis:
- [IPinfo.io](https://ipinfo.io/)
- [URLScan.io](https://urlscan.io/)
- [Talos Reputation Center](https://talosintelligence.com/reputation)
- [CyberChef](https://gchq.github.io/CyberChef/)
- [ConvertCSV URL Extractor](https://www.convertcsv.com/url-extractor.htm)

### Tools for File Hash & Attachment Analysis:
- `sha256sum` command
- [VirusTotal](https://www.virustotal.com/gui/)
- [Talos File Reputation](https://talosintelligence.com/talos_file_reputation)
- ReversingLabs (file reputation)

## 🧪 Malware Sandbox Services
- [Any.Run](https://app.any.run/)
- [Hybrid Analysis](https://www.hybrid-analysis.com/)
- [Joe Sandbox](https://www.joesecurity.org/)

These sandboxes help determine:
- Network connections
- Downloaded payloads
- IOCs (Indicators of Compromise)
- Persistence mechanisms

## 🛠 PhishTool for Automated Analysis

- Combines metadata, OSINT, and automated threat analysis
- Free Community Edition available
- Features:
  - Email sender/recipient/timestamp
  - IP & DNS lookup
  - SMTP relay trace (Hop data)
  - View email body (text/HTML)
  - Auto-extract URLs and attachments
  - VirusTotal API integration
  - Resolve & flag emails with notes and classification codes

## 🏷️ Classification Codes

Used for tagging phishing cases. Examples:
- Whaling (targeting executives like CFOs)

---

**Note:** Always consider deeper analysis like domain origin research and sandboxing attachments for complete understanding of threats.


![image](https://github.com/user-attachments/assets/d2ac1dc0-cbe9-4083-8dca-6688e4d38ed8)
