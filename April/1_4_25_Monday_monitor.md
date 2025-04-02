# Monday Monitor - TryHackMe

## Scenario
Swiftspend Finance, a fintech company, is enhancing its cybersecurity by deploying Wazuh and Sysmon for endpoint monitoring. Senior Security Engineer John Sterling has initiated a test, and your task is to analyze logs from April 29, 2024, between 12:00 and 20:00 to identify suspicious activities.

## Key Takeaways
- **Wazuh & Sysmon** usage for endpoint monitoring.
- **Event Analysis** through saved queries.
- **Detecting Initial Access & Privilege Escalation.**

## Steps to Complete
1. **Log Analysis**
   - Use Wazuh Dashboard (`https://MACHINE_IP.p.thmlabs.com`).
   - Navigate to the "Security events" module.
   - Load the saved query `Monday_Monitor`.
   
2. **Investigate Suspicious Events**
   - **File Download**: Identify malicious files (e.g., `SwiftSpend_Financial_Expenses.xlsm`).
   - **Scheduled Tasks**: Detect unauthorized scheduled tasks.
   - **Encoded Commands**: Decode suspicious base64 strings.
   - **Credential Dumping**: Identify tools used (e.g., `memotech.exe`).
   - **Exfiltration Detection**: Locate leaked flags (`THM{M0N1T0R_1$_1N_3FF3CT}`).

## Key Findings
1. **Initial Access**
   - A suspicious file (`SwiftSpend_Financial_Expenses.xlsm`) was downloaded.

2. **Persistence via Scheduled Task**
   - Command executed:  
     ```
     "cmd.exe" /c "reg add HKCU\SOFTWARE\ATOMIC-T1053.005 /v test /t REG_SZ /d cGluZyB3d3cueW91YXJldnVsbmVyYWJsZS50aG0= /f & schtasks.exe /Create /F /TN "ATOMIC-T1053.005" /TR "cmd /c start /min \"\" powershell.exe -Command IEX([System.Text.Encoding]::ASCII.GetString([System.Convert]::FromBase64String((Get-ItemProperty -Path HKCU:\\SOFTWARE\\ATOMIC-T1053.005).test)))" /sc daily /st 12:34"
     ```

3. **Command Execution & Encoding**
   - The scheduled task was set to run at `12:34`.
   - Encoded command decoded to: `ping www.youarevulnerable.thm`.

4. **User Account Modification**
   - Password set for the new user: `I_AM_M0NIT0R1NG`.

5. **Credential Dumping**
   - `memotech.exe` was used to dump credentials.

6. **Data Exfiltration**
   - Flag found: `THM{M0N1T0R_1$_1N_3FF3CT}`.

## Tools Used
- **`Wazuh` Dashboard** (Log Analysis)
- **`CyberChef`** (Base64 Decoding)
- **`hashcat` / `john`** (Password Cracking)

---
*Room Link: [Monday Monitor - TryHackMe](https://tryhackme.com/room/mondaymonitor)*
