# Crack the Hash

## Task 1: Level 1

### Hash: `48bb6e862e54f2a795ffc4e541caed4d`
- **Type:** MD5
- **Command:** `hashcat -m 0 hash1_1.txt /usr/share/wordlists/rockyou.txt --show`
- **Cracked Password:** `easy`

### Hash: `CBFDAC6008F9CAB4083784CBD1874F76618D2A97`
- **Type:** SHA1
- **Command:** `hashcat -m 100 hash1_2.txt /usr/share/wordlists/rockyou.txt --show`
- **Cracked Password:** `password123`

### Hash: `1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032`
- **Type:** SHA256
- **Command:** `hashcat -m 1400 hash1_3.txt /usr/share/wordlists/rockyou.txt --show`
- **Cracked Password:** `letmein`

### Hash: `$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom`
- **Type:** bcrypt
- **Command:** `hashcat -m 3200 hash1_4.txt /usr/share/wordlists/rockyou.txt`
- **Cracked Password:** `bleh`

### Hash: `279412f945939ba78ce0758d3fd83daa`
- **Type:** MD4
- **Command:** `hashcat -m 900 hash1_5.txt /usr/share/wordlists/rockyou.txt`
- **Cracked Password:** `Eternity22`

---

## Task 2: Level 2

### Hash: `F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85`
- **Type:** SHA256
- **Command:** `hashcat -m 1400 hash2_1.txt /usr/share/wordlists/rockyou.txt`
- **Cracked Password:** `paule`

### Hash: `$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.`
- **Salt:** aReallyHardSalt
- **Rounds:** 5
- **Type:** NTLM
- **Command:** `hashcat -m 1000 hash2_2.txt /usr/share/wordlists/rockyou.txt`
- **Cracked Password:** `n63umy8lkf4i`

### Hash: `e5d8870e5bdd26602cab8dbe07a942c8669e56d6`
- **Salt:** tryhackme
- **Type:** SHA-512(Unix)
- **Command:** `hashcat -m 1800 hash2_3.txt /usr/share/wordlists/rockyou.txt`
- **Cracked Password:** `waka99`

### Hash: `e5d8870e5bdd26602cab8dbe07a942c8669e56d6`
- **Salt:** tryhackme
- **Type:** HMAC-SHA1
- **Command:** `hashcat -m 160 hash2_4.txt /usr/share/wordlists/rockyou.txt`
- **Cracked Password:** `481616481616`
