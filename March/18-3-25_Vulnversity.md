
## Reconnaissance  

### Nmap - Network Scanning  
- **Nmap** is used to discover hosts and services in a network.  
- **Key flags:**  
  - `-sV` → Detect service versions.  
  - `-p <x>` or `-p-` → Scan specific or all ports.  
  - `-Pn` → Disable host discovery, scan directly.  
  - `-A` → OS detection, script execution.  
  - `-sC` → Scan with default scripts.  
  - `-sU` → UDP scan, `-sS` → TCP SYN scan.  

### Gobuster - Directory & File Enumeration  
- **Gobuster** is a brute-force tool for directories, files, and subdomains.  
- **Usage:**  
  - Requires a wordlist (e.g., `/usr/share/wordlists/dirbuster/directory-list-1.0.txt`).  
  - Run:  
    ```bash
    gobuster dir -u http://MACHINE_IP:3333 -w <wordlist>
    ```
- **Key flags:**  
  - `-e` → Print full URLs.  
  - `-u` → Target URL.  
  - `-w` → Path to wordlist.  
  - `-p <x>` → Use proxy for requests.  
  - `-c <cookies>` → Use authentication cookies.  

---

## Exploitation  

### File Upload & BurpSuite Intruder  
- **Fuzzing upload forms** to find allowed file extensions.  
- **BurpSuite Intruder**: Automates payload-based attacks.  
- **Common test extensions:**: .php, .php3, .php4, .php5, .phtml

  - **Steps:**  
1. Capture file upload request in BurpSuite.  
2. Use Intruder → "Sniper" mode → Add extension variations.  
3. Find an accepted extension for shell upload.  

### Reverse Shell Execution  
- **Goal:** Gain remote access to the target machine.  
- **Steps:**  
1. Edit `php-reverse-shell.php`, set **attacker's tun0 IP**.  
2. Rename file to `php-reverse-shell.phtml`.  
3. Start listener:  
   ```bash
   nc -lvnp 1234
   ```
4. Upload & execute shell:  
   ```
   http://MACHINE_IP:3333/internal/uploads/php-reverse-shell.phtml
   ```
5. Capture reverse shell session.  

---

## Privilege Escalation  

### Exploiting SUID Binaries  
- **SUID (Set User ID)**: Allows executing files with owner's privileges (e.g., root).  
- **Example:** `/usr/bin/passwd` modifies shadow files needing root access.  
- **Finding SUID binaries:**  
```bash
find / -perm -u=s -type f 2>/dev/null


Possible escalation:
Exploit misconfigured SUID binaries to execute commands as root.

