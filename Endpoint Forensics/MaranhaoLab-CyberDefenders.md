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

The user fell for a social engineering attack, downloading what they thought was 'Fnafdoomlauncher' from a Google Drive link. Once opened, the malware didn't just run once; it dug in by hiding a fake 'Updater' program in the user's local AppData folder and modifying the Registry to make sure it survived a reboot.

Before doing any damage, it played it safe—using standard Windows commands (wmic) to look around and verify it was on a real machine rather than a security researcher's sandbox. The smoking gun came at the end: it forcibly killed the user's browser and opened a specific named pipe (ChromeDecryptIPC). That’s a clear signal it was hooking into the browser processes to scrape saved passwords and session cookies before sending that data out to its command-and-control server

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

**Explanation:** Review sysmon logs for event id 1 and filter for Fnafdoomlauncher

> <img width="803" height="66" alt="Q4" src="https://github.com/user-attachments/assets/a8444cf4-f470-4900-be1b-95b9d1e798db" />
---

### Task 5
**Question:** Forensic correlation across endpoints requires file-level fingerprinting. What SHA1 hash uniquely represents the dropper binary that initiated further payload deployment?

**Answer:** `FCB94C06FA80CE277B47E545B3805AB38BB6ACF4`

**Explanation:** the above log provides the inital dropper Fnafdoomlauncher.tmp

> <img width="1717" height="36" alt="Q5" src="https://github.com/user-attachments/assets/03d58a70-84e2-4bd1-939d-f36e31e4fc09" />
---

### Task 6
**Question:** Post-installation, the secondary payload did not remain in temporary directories but was staged in a user-space program folder. Identify the exact directory path used for this execution pivot.

**Answer:** `C:\Users\Levi\AppData\Local\Programs\Microsoft Updater\`

---

### Task 7
**Question:** During execution, the secondary component was invoked with a victim-tagging token for C2 identification. What globally unique string was provided as the argument?

**Answer:** `e90de8b2-eb79-4614-94f8-308f0f81573b`

**Explanation:** Review sysmon event id 1 logs. This will provide file creation even where the command is ""C:\Users\Levi\AppData\Local\Programs\Microsoft Updater\updater.exe" e90de8b2-eb79-4614-94f8-308f0f81573b"

> <img width="772" height="445" alt="Q7" src="https://github.com/user-attachments/assets/3a8d475b-db49-4213-8350-b0ea9fa33579" />
---

### Task 8
**Question:** What was the complete file path of the binary embedded within the persistence mechanism to guarantee re-execution after reboot?

**Answer:** `C:\Users\Levi\AppData\Local\Programs\Microsoft Updater\Updater.exe`

**Explanation:** Review sysmon logs for event id 1 and filter for reg.exe to review creation of registry keys

> <img width="3241" height="24" alt="Q8" src="https://github.com/user-attachments/assets/66e5f862-940f-4bf8-9243-ed0cb0446e84" />
---

### Task 9
**Question:** Temporal analysis of registry modifications showed the exact moment persistence was locked in. What is the date and time this key entry was created?

**Answer:** `2025-09-17 10:13`

**Explanation:** Above logs provides this info

---

### Task 10
**Question:** Post-installation, the adversary concealed its artifacts at the file-system level. Which native Windows utility and attribute combination was used to render both files and directories hidden and system-protected?

**Answer:** `attrib +h +s`

**Explanation:** Reviewing same Sysmon event id 1 this would provide proof for these these command

> <img width="766" height="76" alt="Q10" src="https://github.com/user-attachments/assets/d8a7ee61-6586-475a-b2b9-5ab11664742c" />
---

If you filter sysmon event id 1 and for cmd.exe you would find multiple discovery commands being run. below image provides all the discovery commands that where run by updater.exe

> <img width="2262" height="324" alt="Q11-Q16" src="https://github.com/user-attachments/assets/4cb9fc5e-95d4-40bf-925e-905d127ba1e2" />

### Task 11
**Question:** Investigators observed the malware pulling system-level metadata that revealed the installed edition of Windows (e.g., "Microsoft Windows 10 Pro"). This information could later be used by the attacker to determine compatibility with payload execution. Which exact query facilitated this operating system enumeration?

**Answer:** `wmic os get Caption`

---

### Task 12
**Question:** To assess whether the compromised system had sufficient processing resources or was running in a sandbox with emulated hardware, the malware issued a command to extract the processor's vendor and model string. What specific query enabled this reconnaissance?

**Answer:** `wmic cpu get Name`

---

### Task 13
**Question:** As part of its environment fingerprinting, the malware attempted to identify graphics hardware to help distinguish between a physical workstation and a low-resource virtual machine. Which query would return the video controller model?

**Answer:** `wmic path win32_VideoController get Name`

---

### Task 14
**Question:** The malware generated a unique victim identifier that would remain stable across reboots and reinstalls by retrieving a machine's hardware UUID. Which WMI command was responsible for collecting this globally unique identifier?

**Answer:** `wmic csproduct get UUID`

---

### Task 15
**Question:** During host triage, analysts identified a query that enumerated logical drives along with their free space and size. This could help an attacker determine whether the host was worth further exploitation (e.g., data exfiltration feasibility). Which WMI command produced this disk inventory?

**Answer:** `wmic logicaldisk get Caption,FreeSpace,Size,Description /format:list`

---

### Task 16
**Question:** Unlike transient licensing tokens stored in tokens.dat, the malware pursued a static registry artifact used as a backup for Windows activation. Identify the precise registry entry (hive, key path, and value) that serves as a fallback product key reference.

**Answer:** `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform\BackupProductKeyDefault`

---

### Task 17
**Question:** Attackers often terminate browsers before attempting to steal session data, cookies, or inject a malicious browser extension. What is the command that was used to forcibly terminate all browser processes?

**Answer:** `taskkill  /F /IM msedge.exe`

**Explanation:** Reviewing same set of above logs would provide this command thats terminating edge browser

> <img width="1713" height="251" alt="Q17" src="https://github.com/user-attachments/assets/f0d31cad-f0ed-4a9b-ab53-58af1703b951" />
---

### Task 18
**Question:** After injection, the malware established an interprocess channel for credential theft. What named pipe was created to ferry stolen browser data?

**Answer:** `ChromeDecryptIPC_e7e223c5-50d5-40ae-8513-64c9962789c2`

**Explanation:** Filter for Sysmon logs event Id 17. Upon reviewing these logs for pipes created you will find "ChromeDecryptIPC" this is the only one for browser IPC.

> <img width="673" height="175" alt="Q18" src="https://github.com/user-attachments/assets/983a32fb-3725-4f82-adca-cf7a2e9a5b54" />
---

### Task 19
**Question:** To enrich host discovery with geolocation data, the malware beaconed to an external resolver. Which service endpoint did it query?

**Answer:** `ip-api.com`

**Explanation:** Review sysmon event id 22 for dns queries and filter for malware "updater.exe" this will provide domain the malware is beaconing to and its associated ip address.

> <img width="2375" height="24" alt="Q1920" src="https://github.com/user-attachments/assets/a15b312e-2024-48c2-8ccd-7fd19b337379" />
---

### Task 20
**Question:** Blocking by domain is insufficient; analysts confirmed the resolved address of the geolocation API. Which single IP must be blacklisted?

**Answer:** `208.95.112.1`

---

### Task 21
**Question:** During network traffic analysis, the malware's outbound request did not resolve to a direct host but instead terminated at Cloudflare's edge network, a common tactic to conceal attacker infrastructure. Which two IP addresses were returned as part of this resolution?

**Answer:** `172.67.144.96, 104.21.71.100`

**Explanation:** Reviewing other Dns queries by updater.exe. You will find the two ips that were returned.

> <img width="2356" height="106" alt="Q21" src="https://github.com/user-attachments/assets/4f8725fa-a588-44b6-bc92-d71964b5f1d6" />
---







