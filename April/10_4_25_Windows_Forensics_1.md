# Windows Forensics Tasks Summary

## Task 1: Introduction to Windows Forensics
### 1. What is the most used Desktop Operating System right now?
- **Answer:** Microsoft Windows

## Task 2: Windows Registry and Forensics
### 1. What is the short form for HKEY_LOCAL_MACHINE?
- **Answer:** HKLM

## Task 3: Accessing registry hives offline
### 1. What is the path for the five main registry hives, DEFAULT, SAM, SECURITY, SOFTWARE, and SYSTEM?
- **Answer:** C:\Windows\System32\Config
### 2. What is the path for the AmCache hive?
- **Answer:** C:\Windows\AppCompat\Programs\Amcache.hve

## Task 6: System Information and System Accounts
### 1. What is the Current Build Number of the machine whose data is being investigated?
- **Answer:** 19044
### 2. Which ControlSet contains the last known good configuration?
- **Answer:** 1
### 3. What is the Computer Name of the computer?
- **Answer:** THM-4N6
### 4. What is the value of the TimeZoneKeyName?
- **Answer:** Pakistan Standard Time
### 5. What is the DHCP IP address?
- **Answer:** 192.168.100.58
### 6. What is the RID of the Guest User account?
- **Answer:** 501

## Task 7: Usage or knowledge of files/folders
### 1. When was EZtools opened?
- **Answer:** 2021-12-01 13:00:34
### 2. At what time was My Computer last interacted with?
- **Answer:** 2021-12-01 13:06:47
### 3. What is the Absolute Path of the file opened using notepad.exe?
- **Answer:** C:\Program Files\Amazon\Ec2ConfigService\Settings
### 4. When was this file opened?
- **Answer:** 2021-11–30 10:56:19

## Task 8: Evidence of Execution
### 1. How many times was the File Explorer launched?
- **Answer:** 26
### 2. What is another name for ShimCache?
- **Answer:** AppCompatCache
### 3. Which of the artifacts also saves SHA1 hashes of the executed programs?
- **Answer:** AmCache
### 4. Which of the artifacts saves the full path of the executed programs?
- **Answer:** BAM/DAM

## Task 9: External Devices/USB device forensics
### 1. What is the serial number of the device from the manufacturer ‘Kingston’?
- **Answer:** IC6F654E59A3B0C179D366AE&0
### 2. What is the name of this device?
- **Answer:** Kingston DataTraveler 2.0 USB Device
### 3. What is the friendly name of the device from the manufacturer ‘Kingston’?
- **Answer:** USB

## Task 10: Hands-on Challenge
1. **How many user created accounts are present on the system?**
   - **Answer:** 3
2. **What is the username of the account that has never been logged in?**
   - **Answer:** thm-user2
3. **What’s the password hint for the user THM-4n6?**
   - **Answer:** count
4. **When was the file ‘Changelog.txt’ accessed?**
   - **Answer:** 2021–11–24 18:18:48
5. **What is the complete path from where the python 3.8.2 installer was run?**
   - **Answer:** Z:\setups\python-3.8.2.exe
6. **When was the USB device with the friendly name ‘USB’ last connected?**
   - **Answer:** 2021–11–24 18:40:06
