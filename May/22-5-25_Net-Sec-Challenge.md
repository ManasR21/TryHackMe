# TryHackMe: Net Sec Challenge Writeup

## Question 2.1

**What is the highest port number being open less than 10,000?**
**Answer:** `8080`

### 🔍 Command:

```bash
nmap -sS -vv -sV -p1-10000 <target>
```

* `-sS`: TCP SYN scan for stealth
* `-vv`: Increase verbosity
* `-sV`: Version detection
* `-p1-10000`: Scan ports from 1 to 10000

---

## Question 2.2

**There is an open port outside the common 1000 ports; it is above 10,000. What is it?**
**Answer:** `10021`

### 🔍 Command:

```bash
nmap -p- <target>
```

* `-p-`: Scan all 65535 ports

---

## Question 2.3

**How many TCP ports are open?**
**Answer:** `6`

### 🔍 Command:

```bash
nmap -sS -sV -p- <target>
```

* Helps count the number of open TCP ports with version detection

---

## Question 2.4

**What is the flag hidden in the HTTP server header?**
**Answer:** `THM{web_server_25352}`

### 🔍 Command:

```bash
nmap -sV --script=http-headers -p80 <target>
```

* Scans HTTP headers for hidden information on port 80

---

## Question 2.5

**What is the flag hidden in the SSH server header?**
**Answer:** `THM{946219583339}`

### 🔍 Command:

```bash
nmap --script ssh2-enum-algos -sV -p22 <target>
```

* Enumerates supported SSH algorithms; can reveal header info

---

## Question 2.6

**We have an FTP server listening on a nonstandard port. What is the version of the FTP server?**
**Answer:** `vsftpd 3.0.3`

### 🔍 Command:

```bash
nmap -sV -p- <target>
```

* `-sV` reveals the version info
* Used during full port scan

---

## Question 2.7

**We learned two usernames (eddie, quinn). What is the flag in one of their FTP accounts?**
**Answer:** `THM{321452667098}`

### 🔍 Commands:

```bash
hydra -l eddie -P rockyou.txt ftp://<target>:10021
hydra -l quinn -P rockyou.txt ftp://<target>:10021 -v
```

* Brute force login for eddie and quinn

```bash
ftp <target> 10021
```

* Logged in via FTP and retrieved `ftp_flag.txt`

---

## Question 2.8

**Solve the challenge on http\://<target>:8080 to get the flag.**
**Answer:** `THM{f7443f99}`

### 🔍 Command:

```bash
nmap -sN <target>
```

* `-sN`: Null scan (no flags) to attempt stealth and IDS evasion

---



