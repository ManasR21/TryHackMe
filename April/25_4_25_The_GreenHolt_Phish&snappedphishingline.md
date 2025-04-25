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





# Task: An Ordinary Midsummer Day - Phishing Investigation

## ⚠️ Disclaimer
This scenario is based on real-world events.  
**Caution**: The phishing kit is from an actual campaign. Interact with it **only within the provided VM** to ensure safety.

---

## 🧑‍💻 Incident Background

You are an IT staff member at **SwiftSpend Financial**.  
Several employees received a suspicious email — some submitted credentials and lost access.  
Your role is to investigate:

- Analyze email samples
- Investigate phishing URLs
- Retrieve and inspect the phishing kit
- Use CTI tools to gather threat intel

---

## 🖥️ Virtual Machine Access

| Field | Value |
|-------|-------|
| **Username** | `damianhall` |
| **Password** | `Phish321` |
| **Directory** | `~/Desktop/phish-emails` |

Use the VM (split view or RDP) to complete the analysis. Tools like **Firefox**, **text editors**, and **grep** will help.

---

## 📬 Email and Phishing Kit Analysis

| Question | Answer |
|----------|--------|
| **Who received a PDF attachment?** | `William McClean` |
| **Adversary's sender email?** | `Accounts.Payable@groupmarketingonline.icu` |
| **Phishing redirection URL (Zoe Duncan)** | `hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error` |
| **Phishing kit .zip archive URL** | `hxxp[://]kennaroads[.]buzz/data/Update365[.]zip` |
| **SHA256 hash of phishing kit** | `ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686` |
| **Phishing kit first submitted** | `2020-04-08 21:55:50 UTC` |
| **SSL certificate first logged** | `2020-06-25` |
| **Email that submitted password twice** | `michael.ascot@swiftspend.finance` |
| **Adversary’s credential collection email** | `m3npat@yandex.com` |
| **Additional adversary email (@gmail.com)** | `jamestanner2299@gmail.com` |
| **Hidden flag** | `THM{pL4y_w1Th_tH3_URL}` |

---

## ✅ Conclusion

This phishing campaign:
- Used fake payment department emails
- Employed redirection to steal credentials
- Collected sensitive info via a hosted phishing kit

> **Actionable Recommendation**: Improve email filtering, educate staff, and monitor for leaked credentials across internal and external systems.

