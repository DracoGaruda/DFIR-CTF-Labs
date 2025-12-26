# DFIR Report: RevengeHotelsAPTLab

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-25 |
| **Platform** | Windows |
| **Tasks** | 15 |


## 1. Scenario

*On September 28, 2025, the SOC team detected suspicious network activity from an administrator's workstation, including connections to an unknown external IP address and unauthorized security tool modifications. The user reported opening what appeared to be a legitimate document received via email earlier that day, after which their security software was mysteriously disabled.

Initial triage reveals evidence of file creation in unusual locations and system configuration changes, suggesting a multi-stage attack with potential data exfiltration occurring hours after the initial compromise.

You have been provided with a disk triage of the compromised host. Your mission is to reconstruct the complete attack chain, identify all malicious components, and determine the full scope of the compromise*

## 2. Summary
*Summary of the incident goes here.*

## 3. Challenge Solutions

### Task 1
**Question:** During the initial compromise, the threat actor distributed a phishing email containing a URL pointing to a malicious JavaScript file disguised as a legitimate document. What is the name of the JavaScript file downloaded from the phishing link?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 2
**Question:** The malicious JavaScript payload was hosted on a compromised website to facilitate the initial infection. What is the complete domain name that hosted the malicious JS file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 3
**Question:** The JavaScript file created a PowerShell script to advance the attack chain. What is the full directory path where the PowerShell script was created from the JS file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 4
**Question:** The PowerShell script invoked another PowerShell command to download two additional files onto the device and then executed one of them. What are the names of the downloaded files?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 5
**Question:** The downloaded files included obfuscated content that needed to be converted to reveal their true nature. What is the actual file type of the second downloaded file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** The first downloaded file converted the second file to its original format, saved it, and then executed it. What is the name of the executed file that was run after conversion?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** The initial JavaScript file employed specific technique to evade security controls and prevent detection. What is the MITRE ATT&CK technique ID for the method used by the JavaScript file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** The malicious executable modified multiple security-related registry keys to weaken system defenses. How many registry keys were edited by the malicious executable?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** The malicious executable established communication with a C2 server infrastructure. What is the IP address of the C2 server that the malicious executable contacted?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** As part of its persistence strategy, the malware created a copy of itself in a different location. What is the full path where the malware copied itself?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 11
**Question:** To maintain persistence after system reboots, the executable added an entry to a specific registry location. What is the full path of the registry key where the executable added its persistence mechanism?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 12
**Question:** A VBS script was deployed as an additional persistence mechanism to maintain the malware's presence. What is the name of the VBS script executed by the malicious executable for persistence?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 13
**Question:** To ensure the malware process couldn't be terminated easily, it used a specific Windows API function to mark itself as critical. What Windows API function does the malicious executable use to mark its process as critical to the system?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** The threat actor deployed an additional executable specifically designed for data collection activities. What is the name of the executable dropped for data collection purposes?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** ter gathering sensitive data, the malware compressed the collected information into an archive for exfiltration. What is the exact timestamp when the collected data archive was created?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---


