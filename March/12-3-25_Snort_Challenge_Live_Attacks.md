# TryHackMe Snort Challenge Summary

## Objective
Analyze network traffic using Snort to detect and investigate brute-force attacks and reverse-shell activities.

---

## Task 1: Brute-Force Attack Detection

### Approach:
- Identified multiple SSH connection attempts in the `snort.log` file.
- Detected brute-force patterns from the attacker's IP: `192.168.1.100`.
- Number of failed SSH attempts: **50**.
- Successfully flagged by Snort using pre-configured SSH brute-force detection rules.

### Snort Rule Example:
```shell
alert tcp any any -> any 22 (msg:"SSH Brute Force Attempt"; flags:S; threshold:type threshold, track by_src, count 5, seconds 60; sid:1000001; rev:1;)
```
---

## Task 2: Reverse Shell Detection

### Approach:
- Analyzed unusual outbound traffic patterns.
- Detected a reverse shell from victim machine `192.168.1.150` to attacker IP `192.168.1.200` on port `4444`.
- Identified the use of Netcat for reverse shell communication.

### Snort Rule Example:
```shell
alert tcp any any -> any 4444 (msg:"Reverse Shell Detected"; content:"nc"; sid:1000002; rev:1;)
```
