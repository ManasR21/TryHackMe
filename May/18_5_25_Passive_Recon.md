![image](https://github.com/user-attachments/assets/9269ade9-7488-48d7-87bc-7547aa900185)

# Reconnaissance and Information Gathering

## Introduction

Sun Tzu once said, *"If you know the enemy and know yourself, your victory will not stand in doubt."* This principle applies well to cybersecurity. Both attackers and defenders benefit from understanding systems through reconnaissance.

Reconnaissance (recon) is the first step in the Unified Kill Chain, involving information gathering on a target system or network to gain an initial foothold.

## Types of Reconnaissance

### Passive Reconnaissance

* Relies on publicly available data
* Does **not** involve direct interaction with the target
* Examples:

  * Checking DNS records using public DNS servers
  * Reading company job postings
  * Reviewing news articles about the target company

### Active Reconnaissance

* Involves **direct interaction** with the target
* May be intrusive and legally risky without authorization
* Examples:

  * Connecting to company servers (HTTP, FTP, SMTP)
  * Social engineering (e.g., phone calls)
  * Physical access attempts (e.g., posing as a repairman)

---

## WHOIS Protocol

WHOIS is a TCP protocol (port 43) defined in RFC 3912 used to get domain registration details.

### Key Data from WHOIS:

* Registrar name
* Registrant contact details (may be hidden)
* Domain creation, update, and expiration dates
* Name servers for the domain

Use local WHOIS clients (on AttackBox, Kali, or Parrot) for faster access.

---

## DNS Lookup Using nslookup

`nslookup` is used to find DNS information about a domain.

### Syntax

```bash
nslookup [OPTIONS] DOMAIN_NAME [SERVER]
```

### Common Query Types:

| Query Type | Purpose            |
| ---------- | ------------------ |
| A          | IPv4 Address       |
| AAAA       | IPv6 Address       |
| MX         | Mail Servers       |
| CNAME      | Canonical Name     |
| SOA        | Start of Authority |
| TXT        | Text Records       |

### Examples

```bash
nslookup -type=A tryhackme.com 1.1.1.1
nslookup -type=MX tryhackme.com
```

These can help identify services and potential attack surfaces.

---

## Advanced DNS Lookup with dig

`dig` (Domain Information Groper) offers more detailed DNS responses.

### Syntax

```bash
dig [@SERVER] DOMAIN_NAME [TYPE]
```

Example:

```bash
dig @1.1.1.1 tryhackme.com MX
```

Returns similar results as `nslookup` but includes additional metadata like TTL (Time To Live).

---

## Subdomain Discovery

DNS tools like `nslookup` and `dig` don't reveal subdomains. Alternatives:

### Methods:

* **Search Engines**: Combine results from multiple engines
* **Brute-force**: Try common subdomain names
* **Online Tools**:

  * **DNSDumpster**: Finds subdomains, DNS data, graphs, and server information

---

## Shodan.io for Passive Reconnaissance

**Shodan.io** scans the internet for connected devices and services, indexing them by:

* IP address
* Hosting company
* Geolocation
* Server software and version

Search for:

* Domains (e.g., `tryhackme.com`)
* IP addresses obtained from DNS queries

Useful for both **attackers** (information gathering) and **defenders** (asset discovery and exposure checks).

---

## Summary

Reconnaissance is the foundation of cybersecurity offense and defense. Understanding how to use tools like WHOIS, `nslookup`, `dig`, DNSDumpster, and Shodan.io can reveal valuable information about a target while staying within legal boundaries during passive recon. Each discovery step builds towards better security posture or more precise targeting, depending on your role.
