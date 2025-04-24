![image](https://github.com/user-attachments/assets/bc3d6b6e-a22c-4840-a1c8-f4befa6bb3c2)

## Task 1: Introduction
Defenders can use multiple strategies to protect users from malicious emails:
- **SPF, DKIM, DMARC**: Authentication protocols to verify the legitimacy of emails.
- **SPAM Filters**: Identify and block potentially harmful emails.
- **Email Labels**: Warn users about emails from external sources.
- **Email/Domain/URL Blocking**: Prevent emails from known malicious sources.
- **Attachment Blocking/Sandboxing**: Stop or test file attachments for threats.
- **Security Awareness Training**: Educate users through simulated phishing attempts.

**Focus Area**: SPF, DKIM, DMARC – foundational to preventing phishing.

**Question 1**  
**Q**: What is the MITRE ID for “Software Configuration”?  
**A**: `M1054`

---

## Task 2: SPF (Sender Policy Framework)

SPF validates if a mail server is allowed to send on behalf of a domain, using DNS TXT records.

**SPF Record Example**:  
`v=spf1 ip4:192.168.0.1 include:_spf.google.com -all`

**Key Mechanisms**:
- `v=spf1`: Version
- `ip4`: Authorized IP
- `include`: Authorized domain
- `-all`: Reject all others

**Questions**  
**Q1**: What prefix character causes a "softfail"?  
**A**: `~`  
**Q2**: What does `-all` mean?  
**A**: `fail`

---

## Task 3: DKIM (DomainKeys Identified Mail)

DKIM ensures emails haven’t been tampered with and verifies the sender domain using cryptographic signatures.

**Typical Record Elements**:
- `v=DKIM1`
- `k=rsa`
- `p=public_key`

**Question 1**  
**Q**: Which email header shows DKIM result?  
**A**: `Authentication-Results`

---

## Task 4: DMARC (Domain-based Message Authentication, Reporting, and Conformance)

DMARC builds on SPF and DKIM for alignment and reporting. Helps detect and prevent spoofing.

**DMARC Record Example**:  
`v=DMARC1; p=quarantine; rua=mailto:postmaster@website.com`

**Question 1**  
**Q**: Which DMARC policy blocks emails on failure?  
**A**: `p=reject`

---

## Task 5: S/MIME (Secure/Multipurpose Internet Mail Extensions)

S/MIME provides:
- **Digital Signatures**: Confirms sender identity.
- **Encryption**: Secures email content.

**Public Key Infrastructure (PKI)** is used for cert exchange and email security.

**Question 1**  
**Q**: What is nonrepudiation?  
**A**: The uniqueness of a signature prevents the owner of the signature from disowning the signature.

---

## Task 6: SMTP Status Codes (Wireshark Analysis)

Analyze SMTP traffic using packet capture tools like Wireshark.

**Questions**  
**Q1**: SMTP filter for status codes?  
**A**: `smtp.response.code`  
**Q2**: Message for status code 220?  
**A**: `<domain> Service ready`  
**Q3**: Packet number and code for spamhaus block?  
**A**: `156,553`  
**Q4**: Message about mailbox in spamhaus block?  
**A**: `mailbox name not allowed`  
**Q5**: Status code before DATA command?  
**A**: `354`

---

## Task 7: SMTP Traffic Analysis

**Questions**  
**Q1**: What port is SMTP using?  
**A**: `25`  
**Q2**: How many SMTP packets?  
**A**: `512`  
**Q3**: Source IP of SMTP traffic?  
**A**: `10.12.19.101`  
**Q4**: Third file attachment filename?  
**A**: `attachment.scr`  
**Q5**: Last file attachment filename?  
**A**: `.zip`

---

## Task 8: SMTP and C2 Communications

SMTP and POP3 can be used for Command and Control (C2) by threat actors.

**Question 1**  
**Q**: Software using SMTP/POP3 for C2?  
**A**: `Zebrocy`

---

## Task 9: Conclusion

The final task discussed using structured playbooks for incident response.

**Question 1**  
**Q**: What framework was used for the IR process?  
**A**: `NIST`

---
