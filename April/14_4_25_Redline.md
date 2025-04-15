## Task 1: Introduction

### 1. Who created Redline?
**Answer:** FireEye

## Task 2: Data Collection

### Questions:
1. **What data collection method takes the least amount of time?**   
   - **Answer:** Standard Collector

2. **What method would you choose for granular data collection against known indicators like domains, hashes, IP addresses, etc.?**
   - **Answer:** IOC Search Collector

3. **What script would you run to initiate data collection?**
   - **Answer:** RunRedlineAudit.bat

4. **Under which option can you find data collection for Disks and Volumes?**
   - **Answer:** Disk Enumeration

5. **What cache does Windows use to maintain a preference for recently executed code?**
   - **Answer:** Prefetch

## Task 3: The Redline Interface

### 1. Where in the Redline UI can you view information about the Logged in User?
   - **Answer:** System Information

## Task 4: Standard Collector Analysis

### 1. Provide the Operating System detected for the workstation.
   - **Answer:** Windows Server 2019 Standard 17763

### 2. What is the suspicious scheduled task that got created on the victim’s computer?
   - **Answer:** MSOfficeUpdateFa.ke

### 3. Find the message that the intruder left for you in the task.
   - **Answer:** THM-p3R5IStENCe-m3Chani$m

### 4. What is the Event ID # for the new system event created by the intruder?
   - **Answer:** 546

### 5. Provide the message for the Event ID.
   - **Answer:** Someone cracked my password. Now I need to rename my puppy-++-

### 6. Provide the full URL of the website from which the intruder downloaded a file.
   - **Answer:** https://wormhole.app/download-stream/gI9vQtChjyYAmZ8Ody0Au

### 7. Provide the full path where the file was downloaded to including the filename.
   - **Answer:** C:\Program Files (x86)\Windows Mail\SomeMailFolder\flag.txt

### 8. Provide the message the intruder left for you in the file.
   - **Answer:** THM{600D-C@7cH-My-FR1EnD}

## Task 5: IOC Search Collector

### 1. What is the actual filename of the Keylogger?
   - **Answer:** psylog.exe

### 2. What filename is the file masquerading as?
   - **Answer:** THM1768.exe

### 3. Who is the owner of the file?
   - **Answer:** WIN-2DET5DP0NPT\charles

### 4. What is the file size in bytes?
   - **Answer:** 35400

### 5. Provide the full path of where the .ioc file was placed.
   - **Answer:** C:\Users\charles\Desktop\Keylogger-IOCSearch\IOCs\keylogger.ioc

## Task 6: IOC Search Collector Analysis

### 1. Provide the path of the file that matched all the artifacts along with the filename.
   - **Answer:** C:\Users\Administrator\AppData\Local\Temp\8eJv8w2id6IqN85dfC.exe

### 2. Provide the path where the file is located without including the filename.
   - **Answer:** C:\Users\Administrator\AppData\Local\Temp

### 3. Who is the owner of the file?
   - **Answer:** BUILTIN\Administrators

### 4. Provide the subsystem for the file.
   - **Answer:** Windows_CUI

### 5. Provide the Device Path where the file is located.
   - **Answer:** \Device\HarddiskVolume2

### 6. Provide the hash (SHA-256) for the file.
   - **Answer:** 57492d33b7c0755bb411b22d2dfdfdf088cbbfcd010e30dd8d425d5fe66adff4

### 7. What is the real filename of the file based on its hash?
   - **Answer:** psexec.exe

## Task 7: Endpoint Investigation

### 1. Can you identify the product name of the machine?
   - **Answer:** Windows 7 Home Basic

### 2. Can you find the name of the note left on the Desktop for "Charles"?
   - **Answer:** _R_E_A_D___T_H_I_S___AJYG1O_.txt

### 3. What is the name of the Windows Defender service DLL?
   - **Answer:** MpSvc.dll

### 4. The user manually downloaded a zip file from the web. What is the filename?
   - **Answer:** eb5489216d4361f9e3650e6a6332f7ee21b0bc9f3f3a4018c69733949be1d481.zip

### 5. Provide the filename of the malicious executable that was dropped on the user’s Desktop.
   - **Answer:** Endermanch@Cerber5.exe

### 6. Provide the MD5 hash for the dropped malicious executable.
   - **Answer:** fe1bc60a95b2c2d77cd5d232296a7fa4

### 7. What is the name of the ransomware?
   - **Answer:** Cerber
