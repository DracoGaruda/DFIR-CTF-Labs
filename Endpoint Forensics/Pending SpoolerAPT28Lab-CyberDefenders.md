# Pending - DFIR Report: Spooler - APT28 Lab - Pending

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-29 |
| **Platform** | Windows |
| **Tasks** | 15 |

## 1. Scenario

The SOC team was notified by the IT department regarding a potentially compromised workstation recently reassigned to a new government employee named Keela. Upon receiving the workstation, Keela reported unusually slow performance and suspected the system had not been properly cleaned before being handed over. The IT team initiated a routine cleanup but identified indicators of suspicious activity suggesting that the machine, and possibly the department’s website may have been previously compromised.

As a forensics investigator, you have been provided with a disk image of Keela’s workstation. Your task is to perform a comprehensive investigation to uncover any signs of malicious activity, reconstruct the timeline of events, and assess the scope and impact of the potential compromise.

## 2. DFIR Analysis Summary



## 3. Challenge Solutions

### Task 1
**Question:** What is the full name of the previous user of this machine, before it was assigned to Keela?

**Answer:** `Yanisara Denthongkul`

**Explanation:** SAM registry hive tracks accounts. So review SAM registry hive with registry explorer

> <img width="1052" height="252" alt="Q1" src="https://github.com/user-attachments/assets/475eb85b-9849-432f-b0c4-49866f1853b9" />
---

### Task 2
**Question:** The previous user downloaded an archive from a compromised internal website that led to the initial infection. When was this archive successfully downloaded?

**Answer:** `2025-08-10 11:11`

**Explanation:** Review the chrome History db file to review downloads. Browse to C\Users\yanis\AppData\Local\Google\Chrome\User Data\Default review History file.
Upon review you find one file download of HR.zip. Convert start time from Chrome timestamp to Human date.

> <img width="1712" height="388" alt="Q2" src="https://github.com/user-attachments/assets/fb54823c-2c4c-46ad-8526-f92f5027f97c" />
---

### Task 3
**Question:** What is the name of the file executed by the user that initiated the infection chain on this machine?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 4
**Question:** Upon executing the file, an HTA script was executed remotely. What is the name of the temporary copy of this script created on this machine?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 5
**Question:** Two files were created in the temporary directory of the compromised user. What are their names? (Provide in alphabetical order)

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** What is the original filename of first file identified in previous question?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** What is the MITRE ATT&CK technique that corresponds to the method the malicious payload used to load itself?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** Which LOLBin was used to download malicious payload?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** A persistence mechanism was created to execute the malicious payload at every system startup. What is the name assigned to this persistence entry?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** Another Boot or Logon Autostart persistence was configured to execute a DLL payload remotely through the Print Spooler service. What is the MITRE ATT&CK Technique ID associated with this persistence mechanism?

**Answer:** `EdgeUpdate`

**Explanation:** Review run reistry keys for Yanis in NTUser.dat

> <img width="1716" height="239" alt="image" src="https://github.com/user-attachments/assets/8bb0caf0-4e93-45f6-8966-e528bab7bef4" />
---

### Task 11
**Question:** What is the full path of the malicious DLL configured to be loaded through the Print Spooler service?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 12
**Question:** According to the event logs, how many failed attempts to load the persistence DLL were recorded due to the network path not being found?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 13
**Question:** A few days later, the attacker dropped and executed an executable to enumerate possible privilege escalation paths on the machine. What is the filename of this executable?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** The attacker executed a privilege escalation technique by leveraging a Windows Installer file. What is the full path of this installer file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** The attacker successfully gained higher privileges by installing software as SYSTEM. Which registry key needed to be enabled for both the user and the software?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---





