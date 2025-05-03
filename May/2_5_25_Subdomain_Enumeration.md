![image](https://github.com/user-attachments/assets/c13a1706-30ca-46dc-984e-90f7c011a678)

# TryHackMe Room Summary: Subdomain Enumeration

## Task 2: OSINT - SSL/TLS Certificates

When an SSL/TLS certificate is created for a domain by a Certificate Authority (CA), it gets logged in public logs called **Certificate Transparency (CT) logs**. These logs help in detecting malicious or accidentally issued certificates.

**Use case in OSINT:**

* Helps identify subdomains that have had SSL certificates issued.
* Services like [crt.sh](https://crt.sh) allow querying these logs.

**How to use crt.sh:**

* Visit [crt.sh](https://crt.sh)
* Search for a domain (e.g., `example.com`)
* Look through the results to identify all subdomains with issued certificates.

## Task 3: OSINT - Search Engines

Search engines like Google index massive amounts of web pages, including subdomains. By using **Google Dorking**, we can uncover subdomains.

**Useful search operator:**

```bash
site:*.domain.com -site:www.domain.com
```

This shows results for all subdomains of `domain.com` excluding `www.domain.com`.

**Benefits:**

* Easily accessible.
* Can find indexed dev/admin subdomains.

## Task 4: DNS Bruteforce

**DNS Bruteforce** is a technique where many possible subdomains are tried to check if they exist for a domain.

**Tool example: `dnsrecon`**

* It automates bruteforce using a list of common subdomains.
* Makes many DNS queries to check validity.

**Why use it?**

* Finds subdomains not listed in public CT logs or search engines.

## Task 5: OSINT - Sublist3r

**Sublist3r** is an automated OSINT tool for discovering subdomains.

**Benefits:**

* Combines multiple search engine results.
* Fast and easy to use.

**Usage:**

```bash
sublist3r -d example.com
```

**Sources used by Sublist3r:**

* Google
* Yahoo
* Bing
* Baidu
* Netcraft

## Task 6: Virtual Hosts Enumeration (VHost)

Some subdomains might not be accessible via DNS (e.g., dev or admin subdomains). These might be defined in local `/etc/hosts` or available via **virtual host routing**.

**Concept:**

* A server can serve multiple websites based on the `Host` header.
* By fuzzing the `Host` header, we can discover hidden virtual hosts.

**Tool example: `ffuf`**

### Basic FFUF Command:

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt \
     -H "Host: FUZZ.acmeitsupport.thm" \
     -u http://MACHINE_IP
```

**Explanation:**

* `-w`: Specifies wordlist.
* `-H`: Adds custom Host header (with FUZZ keyword).
* `-u`: Target URL.

### Filtering Redundant Results:

Since every request returns a valid result, we filter using the most common page size:

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt \
     -H "Host: FUZZ.acmeitsupport.thm" \
     -u http://MACHINE_IP \
     -fs {size}
```

**-fs {size}**: Filters results with size `{size}` (replace with real number from earlier output).

**Why use VHost enumeration?**

* Finds internal apps and dev portals.
* Can reveal staging environments or admin panels.

---

This summary provides a structured breakdown of multiple methods to enumerate and discover subdomains using OSINT and active probing tools.
