![image](https://github.com/user-attachments/assets/62d45323-4824-431d-a14f-c198c9f99ddd)

# Content Discovery - Summary

## Task 1: What Is Content Discovery?

Content discovery refers to the process of identifying hidden or unlinked content within a web application. This can include directories, files, parameters, subdomains, and endpoints. It is a critical phase of reconnaissance in ethical hacking and penetration testing.

---

## Task 2: Manual Discovery - Robots.txt

* `robots.txt` is a text file located at the root of a website (`example.com/robots.txt`).
* It tells web crawlers which pages or files should not be indexed.
* Can reveal sensitive directories or endpoints that developers wanted to hide.

**Example:**

```
Disallow: /admin/
Disallow: /backup/
```

---

## Task 3: Manual Discovery - Favicon

* A `favicon.ico` file can be fingerprinted using tools like [Shodan](https://www.shodan.io/) or [hashes](https://faviconhash.com/) to identify frameworks, CMS, or specific software used.
* Often located at `/favicon.ico`.

---

## Task 4: Manual Discovery - Sitemap.xml

* A `sitemap.xml` contains URLs intended to be indexed by search engines.
* Provides a map of the site's structure and can expose endpoints or pages not linked publicly.
* Located at `/sitemap.xml`.

---

## Task 5: Manual Discovery - HTTP Headers

* Inspect HTTP headers for valuable information like:

  * Server version
  * Framework info
  * Caching mechanisms
  * Cookies (e.g., session IDs)

**Tool:** `curl -I http://example.com`

---

## Task 6: Manual Discovery - Framework Stack

* Analyze source code, HTTP headers, or URLs to identify the technology stack.
* File extensions (.php, .aspx, .jsp), response headers (e.g., `X-Powered-By`), and JavaScript libraries can help in fingerprinting frameworks.

**Tools:** BuiltWith, Wappalyzer

---

## Task 7: OSINT - Google Hacking / Dorking

* Use advanced Google search queries (dorks) to find hidden or sensitive info.

**Examples:**

```
site:example.com ext:log
inurl:admin site:example.com
```

* Can be used to find exposed files, backups, credentials, etc.

---

## Task 8: OSINT - Wappalyzer

* Browser extension and web tool for fingerprinting websites.
* Reveals CMS, eCommerce platforms, analytics, frameworks, and server info.

---

## Task 9: OSINT - Wayback Machine

* Access old versions of websites through [archive.org/web](https://archive.org/web).
* Reveals previously available endpoints, files, or content no longer public.

---

## Task 10: OSINT - GitHub

* Developers may unintentionally expose secrets (API keys, credentials) in public repos.
* Use GitHub search or tools like `gitrob`, `truffleHog` for automated scanning.

---

## Task 11: OSINT - S3 Buckets

* Amazon S3 buckets may be publicly accessible if misconfigured.
* Enumerate buckets with tools or manual testing: `http://bucket-name.s3.amazonaws.com`
* Leaked files, databases, or backups can be exposed.

---

## Task 12: Automated Discovery

* Tools automate the discovery of hidden content or endpoints using wordlists and fuzzing.

**Common Tools:**

* `ffuf`
* `dirb`
* `dirbuster`
* `gobuster`

**Example:**

```bash
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://example.com/FUZZ
```
