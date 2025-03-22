# TShark Challenge: Investigating Malicious Domains

## Challenge Overview
This challenge involves analyzing a `.pcap` file using `tshark` to identify suspicious domains, check them in VirusTotal, and extract key indicators of compromise (IOCs).

## Steps to Solve the Challenge

### 1. Investigate the Contacted Domains
Use `tshark` to extract all DNS queries from the `teamwork.pcap` file:
```bash
 tshark -r teamwork.pcap -Y "dns.qry.name" -T fields -e dns.qry.name | sort -u
```
Identify the suspicious domain from the results.

### 2. Check the Domain in VirusTotal
- Copy the suspicious domain: `paypal.com4uswebappsresetaccountrecovery.timeseaways.com`.
- Submit it to **VirusTotal**.
- Retrieve the **first submission date**: `2017-04-17 22:52:53 UTC`.

### 3. Identify the Impersonated Service
The domain is impersonating **PayPal**.

### 4. Find the IP Address of the Malicious Domain
Use `tshark` to extract A records (IP addresses) related to the domain:
```bash
tshark -r teamwork.pcap -Y "dns.a" -T fields -e dns.qry.name -e dns.a | sort -u
```
The malicious domain resolves to `184.154.127.226`.

### 5. Extract the Email Address Used
Search for HTTP `POST` requests (where credentials may be submitted):
```bash
tshark -r teamwork.pcap -Y "http.request.method == POST" -T fields -e text
```
Identify the email address used: `johnny5alive[at]gmail[.]com`.

## Answers in Defanged Format
- **Malicious URL:**  
  `hxxp[://]www[.]paypal[.]com4uswebappsresetaccountrecovery[.]timeseaways[.]com/`
- **First Submission to VirusTotal:**  
  `2017-04-17 22:52:53 UTC`
- **Impersonated Service:**  
  `PayPal`
- **Malicious IP Address:**  
  `184[.]154[.]127[.]226`
- **Email Address Used:**  
  `johnny5alive[at]gmail[.]com`

🎉 **Challenge Completed!**
