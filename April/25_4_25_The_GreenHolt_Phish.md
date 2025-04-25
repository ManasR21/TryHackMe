![image](https://github.com/user-attachments/assets/070f911e-c3bc-4953-82e7-3a35cbf67dae)

# Task 1: Just Another Day as a SOC Analyst

## 🖥️ Task Summary
A Sales Executive at Greenholt PLC received a suspicious email with a strange greeting, unexpected money transfer reference, and an unsolicited attachment. He forwarded it to the SOC team for investigation.

The goal: **Determine if the email is legitimate** by analyzing its contents and metadata.

---

## 🛠️ Environment Setup
- **Deploy** the provided virtual machine in split view.
- **Open the `.eml` file** using Thunderbird:
  - Right-click `challenge.eml` → Open With Other Application → Choose **Thunderbird Mail**.

---

##  Email Analysis

| Question | Answer |
|----------|--------|
| **Transfer Reference Number (Subject)** | `09674321` |
| **From (Name)** | `Mr. James Jackson` |
| **From (Email)** | `info@mutawamarine.com` |
| **Reply-To Address** | `info.mutawamarine@mail.com` |
| **Originating IP** | `192.119.71.157` |
| **IP Owner** | `Hostwinds LLC` |
| **SPF Record (Return-Path Domain)** | `v=spf1 include:spf.protection.outlook.com -all` |
| **DMARC Record (Return-Path Domain)** | `v=DMARC1; p=quarantine; fo=1` |
| **Attachment Name** | `SWT_#09674321____PDF__.CAB` |
| **Attachment SHA256 Hash** | `2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f` |
| **Attachment Size** | `400.26 KB` |
| **Actual File Extension** | `RAR` |

---

##  Conclusion
The email exhibits multiple red flags:
- Suspicious greeting and unexpected attachment.
- Mismatch in From and Reply-To addresses.
- The attachment disguises a `.rar` file as a `.cab`, potentially malicious.
- SPF and DMARC indicate the domain is protected, yet the IP belongs to a third party (Hostwinds).

> **Verdict:** This email is likely a phishing attempt and **should not be trusted**.
