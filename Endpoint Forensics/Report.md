# DFIR Report: LFIEscalationLab

| Metadata | Details |
|----------|---------|
| **Date** | 2026-01-03 |
| **Platform** | Windows |
| **Tasks** | 20 |

## 1. Scenario

IT staff reported unusual behavior on a workstation running a web application, triggered by an antivirus detection of a suspicious file. Early indicators suggest the website may have served as the entry point.Your task is to investigate the full scope of the compromise—tracing how the attacker gained access, what actions they performed, and how they established persistence on the system.

## 2. DFIR Summary


## 3. Challenge Solutions

### Task 1
**Question:** The threat actor began by probing the web application for hidden or accessible directories. Which IP address was responsible for this scanning activity?

**Answer:** `218.84.168.131`

**Explanation:**
Review Xampp logs. You will find malicious activity from that particular IP address.

> *Screenshot placeholder*
---

### Task 2
**Question:** When was the threat actor's earliest recorded activity on the compromised website?

**Answer:** `2025-09-07 08:56`

**Explanation:**
Look for first log request for above IP address and convert the time stamp to UTC as the original time is in Japanese timestamp

> *Screenshot placeholder*
---

### Task 3
**Question:** The threat actor rotated his User-Agent multiple times throughout the attack. How many User-Agents did the threat actor use during the first reconnaissance phase of the attack?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 4
**Question:** A vulnerability was discovered in the old version of the website. How many files were read by the threat actor using the discovered vulnerability?

**Answer:** `4`

**Explanation:**
If you review logs with requests for oldsite/. Path traversal vulnerability is exploited to read four filesas shown in the screenshot

> *Screenshot placeholder*
---

### Task 5
**Question:** The threat actor was able to access the MySQL database using credentials from one of the files he accessed earlier. What is the password that the threat actor used to access the MySQL database?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** When did the threat actor first successfully authenticate to the MySQL database?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** After authenticating to the MySQL database, the threat actor targeted a specific database for exfiltration. Which database did he access?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** Which table did the threat actor export from the database?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** On the next day, the threat actor logged into the MySQL database again using a different IP address. What is this IP address?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** The threat actor used SQL commands to create a webshell. What is the full path of this webshell file on the system?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 11
**Question:** The threat actor used a Living-off-the-Land Binary (LOLBin) to hide the webshell. What MITRE ATT&CK technique corresponds to this activity?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 12
**Question:** The threat actor executed a command to download a reverse shell payload from a C2 server. What is the domain used to host this payload?

**Answer:** `wscryss.xyz`

**Explanation:**


> *Screenshot placeholder*
---

### Task 13
**Question:** The reverse shell payload was downloaded to a specific location and executed. What is the full path of this payload?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** After establishing the C2 connection, the threat actor attempted several methods to bypass User Account Control (UAC). One method used a PowerShell script. What is the name of this script?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** The PowerShell script executed shellcode as part of its payload. What is the name of the variable that stores the raw shellcode in the script?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 16
**Question:** After failing to bypass UAC, the threat actor downloaded another binary to authenticate as the compromised user. What is the original filename of this binary?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 17
**Question:** What is the SHA-256 hash of the reverse-shell payload the threat actor uploaded and used with the previously identified binary?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 18
**Question:** Which MITRE ATT&CK technique did the threat actor use to establish persistence through registry modifications that execute a payload upon a program's silent termination?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 19
**Question:** Which program was configured to monitor and execute the threat actor's payload as part of his persistence mechanism?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 20
**Question:** The persistence binary executed once on the compromised system. What was the process ID of this execution?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

