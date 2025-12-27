# DFIR Report: RevengeHotelsAPTLab

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-25 |
| **Platform** | Windows |
| **Tasks** | 15 |


## 1. Scenario

On September 28, 2025, the SOC team detected suspicious network activity from an administrator's workstation, including connections to an unknown external IP address and unauthorized security tool modifications. The user reported opening what appeared to be a legitimate document received via email earlier that day, after which their security software was mysteriously disabled.

Initial triage reveals evidence of file creation in unusual locations and system configuration changes, suggesting a multi-stage attack with potential data exfiltration occurring hours after the initial compromise.

You have been provided with a disk triage of the compromised host. Your mission is to reconstruct the complete attack chain, identify all malicious components, and determine the full scope of the compromise

## 2. Summary

The incident originated from a phishing campaign that directed the user to the compromised domain hotelx.rf.gd, resulting in the download of a malicious JavaScript file named invoice82962.js. Upon execution, this file utilized a PowerShell script located in C:\Users\Public\Scripts to retrieve two intermediate text files, venumentrada.txt and runpe.txt, which were then deobfuscated to launch the primary payload, swchost.exe. To evade detection and secure its operation, the malware employed MITRE ATT&CK technique T1562.001 by disabling real-time monitoring, modifying 12 security-related registry keys, and invoking the RtlSetProcessIsCritical API to prevent the process from being terminated.

Once established, the malware initiated command and control communication with the IP address 3.122.239.15 and ensured persistence through a RunOnce registry key, a backup copy in the AppData Roaming folder, and a VBScript named KOoNLZeCGlnQ.vbs. The attack phase culminated in data exfiltration, facilitated by a secondary tool named Flfs6heTV2lb.exe dropped specifically for collection purposes. The stolen data was compressed into an archive for exfiltration, with the final artifact creation timestamped on September 28, 2025, at 17:16:58.

## 3. Challenge Solutions

### Task 1
**Question:** During the initial compromise, the threat actor distributed a phishing email containing a URL pointing to a malicious JavaScript file disguised as a legitimate document. What is the name of the JavaScript file downloaded from the phishing link?

**Answer:** `invoice82962.js`

**Explanation:** Check for browswer ogsto look for potential downloads*


> <img width="1710" height="207" alt="Q1" src="https://github.com/user-attachments/assets/bc0cbde5-ff0a-484f-bda4-73d0f0dd965a" />
---

### Task 2
**Question:** The malicious JavaScript payload was hosted on a compromised website to facilitate the initial infection. What is the complete domain name that hosted the malicious JS file?

**Answer:** `hotelx.rf.gd`

**Explanation:** Check for the URL for the same record*


> <img width="1715" height="244" alt="Q2" src="https://github.com/user-attachments/assets/290ed30f-d513-4b11-b6f0-cbb4ed7655fa" />

---

### Task 3
**Question:** The JavaScript file created a PowerShell script to advance the attack chain. What is the full directory path where the PowerShell script was created from the JS file?

**Answer:** `C:\Users\Public\Scripts`

**Explanation:** Review the Java script code. You will find code was trying to create a powershell. You can find location of file from the chrome history review


> <img width="810" height="291" alt="Q3" src="https://github.com/user-attachments/assets/09c3daa4-e2fd-45f2-8af7-65afd89fd108" />

---

### Task 4
**Question:** The PowerShell script invoked another PowerShell command to download two additional files onto the device and then executed one of them. What are the names of the downloaded files?

**Answer:** `venumentrada.txt, runpe.txt`

**Explanation:** Review the same directory


> <img width="823" height="228" alt="Q4" src="https://github.com/user-attachments/assets/6cab4573-4f22-495e-95b3-348a0264657f" />

---

### Task 5
**Question:** The downloaded files included obfuscated content that needed to be converted to reveal their true nature. What is the actual file type of the second downloaded file?

**Answer:** `EXE`

---

### Task 6
**Question:** The first downloaded file converted the second file to its original format, saved it, and then executed it. What is the name of the executed file that was run after conversion?

**Answer:** `swchost.exe`

**Explanation:** You can find this file in same directory

---

### Task 7
**Question:** The initial JavaScript file employed specific technique to evade security controls and prevent detection. What is the MITRE ATT&CK technique ID for the method used by the JavaScript file?

**Answer:** `T1562.001`

**Explanation:** When you review java script file you find "-Command Set-MpPreference -DisableRealtimeMonitoring $true". This is inline with Impair Defenses (T1562) technique, often through sub-techniques like Disable or Modify Tools (T1562.001)

---

### Task 8
**Question:** The malicious executable modified multiple security-related registry keys to weaken system defenses. How many registry keys were edited by the malicious executable?

**Answer:** `12`

**Explanation:** review sysmon event id 13 logs and filter for swchost.exe. You will find 12 unique microsoft defender logs.

---

### Task 9
**Question:** The malicious executable established communication with a C2 server infrastructure. What is the IP address of the C2 server that the malicious executable contacted?

**Answer:** `3.122.239.15`

**Explanation:** Review sysmon event id 3 for network connections. filter for payload with swchost to get ip address

> <img width="1715" height="1190" alt="Q9" src="https://github.com/user-attachments/assets/0c16e3d2-ec35-40d5-a065-c32fecf65812" />

---

### Task 10
**Question:** As part of its persistence strategy, the malware created a copy of itself in a different location. What is the full path where the malware copied itself?

**Answer:** `C:\Users\Administrator\AppData\Roaming\host\swchost.exe`

**Explanation:** Look for Sysmon Event ID 11 for swchost.exe


> <img width="1689" height="1108" alt="Q10" src="https://github.com/user-attachments/assets/d2543e13-0265-4adb-9a45-8c0aa1bfe404" />

---

### Task 11
**Question:** To maintain persistence after system reboots, the executable added an entry to a specific registry location. What is the full path of the registry key where the executable added its persistence mechanism?

**Answer:** `HKU\S-1-5-21-403280985-4081385913-4248903659-500\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\svchostAS`

**Explanation:** Filter for runkeys with Sysmon eventid 13 as runkeys are good indicators for persistence


> <img width="1715" height="1188" alt="Q11" src="https://github.com/user-attachments/assets/2aa7232a-aff5-4a6e-a226-b963c1f685a5" />

---

### Task 12
**Question:** A VBS script was deployed as an additional persistence mechanism to maintain the malware's presence. What is the name of the VBS script executed by the malicious executable for persistence?

**Answer:** `KOoNLZeCGlnQ.vbs`

**Explanation:** Filter for sysmon eventid 11 and look for .vbs files


> <img width="1499" height="1187" alt="Q12" src="https://github.com/user-attachments/assets/65ba19fb-adb6-4471-9fb3-105172ad9197" />

---

### Task 13
**Question:** To ensure the malware process couldn't be terminated easily, it used a specific Windows API function to mark itself as critical. What Windows API function does the malicious executable use to mark its process as critical to the system?

**Answer:** `RtlSetProcessIsCritical`


---

### Task 14
**Question:** The threat actor deployed an additional executable specifically designed for data collection activities. What is the name of the executable dropped for data collection purposes?

**Answer:** `Flfs6heTV2lb.exe`


---

### Task 15
**Question:** ter gathering sensitive data, the malware compressed the collected information into an archive for exfiltration. What is the exact timestamp when the collected data archive was created?

**Answer:** `2025-09-28 17:16:58`

**Explanation:** Review sysmonlogs event id 11 for zip file creations


> <img width="1605" height="1188" alt="Q15" src="https://github.com/user-attachments/assets/fa4487f0-4e70-4bff-b56c-4f49d5eefe50" />

---










