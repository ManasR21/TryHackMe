# Summary of Cyber Attack Investigation - Wayne Enterprise

We analyzed a defacement attack on the website `imreallynotbatman.com`, mapping attacker activity across the **Cyber Kill Chain**:

---

## 🔍 1. Reconnaissance
- Attacker IP: `40.80.148.42`
- Used **Acunetix** web scanner to probe the server

---

## 💥 2. Exploitation
- Brute-force attack from IP `23.22.63.114`
- Successful login from `40.80.148.42`
- 142 brute-force attempts; 1 successful

---

## 📦 3. Installation
- Malicious file `3791.exe` uploaded
- MD5 hash retrieved from Sysmon logs

---

## 🎯 4. Action on Objective
- Website defaced post-compromise
- Defacement file identified in server logs

---

## 🧪 5. Weaponization
- Domain used: `prankglassinebracket.jumpingcrab.com`
- IP: `23.22.63.114`
- Masquerading domains linked to attacker
- Email tied to attacker: `Lillian.rose@po1s0n1vy.com`

---

## 🚚 6. Delivery
- Malware identified: `MirandaTateScreensaver.scr.exe`
- MD5 hash: `c99131e0169171935c5ac32615ed6261`

---
