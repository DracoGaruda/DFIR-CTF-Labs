# DFIR Report: MaranhaoLab - In progress

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-26 |
| **Platform** | Windows |
| **Tasks** | 21 |

## 1. Scenario

A gaming enthusiast in a known organization has downloaded what they believed to be a free mod launcher for a popular survival game. The file which downloaded contained a ZIP archive with an installer that looked like a standard game setup package. 

Eager to try it, the gamer downloaded the file and executed the installer. Unbeknownst to him, the program silently dropped hidden files into a directory. One of these files was configured to persist through registry keys, ensuring it would relaunch every time the system started. 

Within a short time, unusual activity triggered alerts on the Security Operations Center's (SOC) in GOAT Company's monitoring dashboard. The gamer's machine was observed making outbound requests to a malicious domain and a suspicious external IP address. Endpoint logs also showed evidence of process injection, suggesting credential theft. The Security Operations Center (SOC) quickly isolated the machine and saved a full disk image for your analysis.

## 2. DFIR Analysis Summary


## 3. Challenge Solutions

### Task 1
**Question:** Analysts identified an external object that acted as the patient-zero delivery mechanism. Which remote resource URL initiated the chain of compromise by providing the archive disguised as a legitimate game utility?

**Answer:** `https://drive.usercontent.google.com/uc?id=1mIxhfZXmcUT2mbKNuahsRI4S_rzVUFKW&export=download`

**Explanation:** Review chrome History log file. Look for URL-downloads. 

> <img width="1712" height="325" alt="Q1" src="https://github.com/user-attachments/assets/5b186164-797d-4746-ade2-65c014b02567" />

---

### Task 2
**Question:** In reconstructing the timeline of compromise, which precise timestamp correlates to the adversary's delivery vector entering the victim environment as a ZIP file?

**Answer:** `2025-09-17 10:10`

**Explanation:** look for the start time of the download from previous log. Convert the timestamp 

> <img width="1713" height="214" alt="Q2" src="https://github.com/user-attachments/assets/b4963e8a-caaa-420e-b166-938c2804d604" />

---

### Task 3
**Question:** The ZIP archive's decompression exposed a loader binary that masqueraded as a legitimate launcher. What was the executable responsible for initializing this staged intrusion?

**Answer:** `Fnafdoomlauncher.exe`

**Explanation:** create MFT csv with zimmerman tools and look for suspcious files after the download of the zip file


> <img width="1717" height="399" alt="Q3" src="https://github.com/user-attachments/assets/e2ffd3c4-1134-4043-8011-fde8ec7cbd8d" />

---

### Task 4
**Question:** Adversaries often alter installer behavior to remain invisible during deployment. Which installer flag was leveraged to suppress user-facing prompts during execution of the trojanized setup?

**Answer:** `/VERYSILENT`

---

### Task 5
**Question:** Forensic correlation across endpoints requires file-level fingerprinting. What SHA1 hash uniquely represents the dropper binary that initiated further payload deployment?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** Post-installation, the secondary payload did not remain in temporary directories but was staged in a user-space program folder. Identify the exact directory path used for this execution pivot.

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** During execution, the secondary component was invoked with a victim-tagging token for C2 identification. What globally unique string was provided as the argument?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** What was the complete file path of the binary embedded within the persistence mechanism to guarantee re-execution after reboot?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** Temporal analysis of registry modifications showed the exact moment persistence was locked in. What is the date and time this key entry was created?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** Post-installation, the adversary concealed its artifacts at the file-system level. Which native Windows utility and attribute combination was used to render both files and directories hidden and system-protected?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 11
**Question:** Investigators observed the malware pulling system-level metadata that revealed the installed edition of Windows (e.g., "Microsoft Windows 10 Pro"). This information could later be used by the attacker to determine compatibility with payload execution. Which exact query facilitated this operating system enumeration?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 12
**Question:** To assess whether the compromised system had sufficient processing resources or was running in a sandbox with emulated hardware, the malware issued a command to extract the processor's vendor and model string. What specific query enabled this reconnaissance?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 13
**Question:** As part of its environment fingerprinting, the malware attempted to identify graphics hardware to help distinguish between a physical workstation and a low-resource virtual machine. Which query would return the video controller model?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** The malware generated a unique victim identifier that would remain stable across reboots and reinstalls by retrieving a machine's hardware UUID. Which WMI command was responsible for collecting this globally unique identifier?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** During host triage, analysts identified a query that enumerated logical drives along with their free space and size. This could help an attacker determine whether the host was worth further exploitation (e.g., data exfiltration feasibility). Which WMI command produced this disk inventory?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 16
**Question:** Unlike transient licensing tokens stored in tokens.dat, the malware pursued a static registry artifact used as a backup for Windows activation. Identify the precise registry entry (hive, key path, and value) that serves as a fallback product key reference.

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 17
**Question:** Attackers often terminate browsers before attempting to steal session data, cookies, or inject a malicious browser extension. What is the command that was used to forcibly terminate all browser processes?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 18
**Question:** After injection, the malware established an interprocess channel for credential theft. What named pipe was created to ferry stolen browser data?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 19
**Question:** To enrich host discovery with geolocation data, the malware beaconed to an external resolver. Which service endpoint did it query?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 20
**Question:** Blocking by domain is insufficient; analysts confirmed the resolved address of the geolocation API. Which single IP must be blacklisted?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 21
**Question:** During network traffic analysis, the malware's outbound request did not resolve to a direct host but instead terminated at Cloudflare's edge network, a common tactic to conceal attacker infrastructure. Which two IP addresses were returned as part of this resolution?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---





