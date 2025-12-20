# DFIR Report: WorkFromHome

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-19 |
| **Platform** | Windows |
| **Tasks** | 25 |

## 1. Executive Summary
*Summary of the incident goes here.*

## 2. Timeline
| Timestamp | Event |
|-----------|-------|
|           |       |

## 3. Challenge Solutions

### Task 1
**Question:** Identify the phishing URL that the user clicked on, resulting in credential harvesting

**Answer:** `http://login.wowzalnc.co.th/logon.php`

**Explanation:**
Check the Chrome browser downloads

![Proof](./screenshots/Task 1.png)
---

### Task 2
**Question:** When did the threat actor gain access to the victim's computer via RDP for the first time?

**Answer:** `2025-05-27 11:59:57`

**Explanation:**
Check in 4624 logs for logon type 10

![Proof](./screenshots/Task 2.png)
---

### Task 3
**Question:** The threat actor accessed several sensitive files on the victim's work-related folder. What is the full path of the PowerPoint presentation file opened by the attacker?

**Answer:** `C:\Users\otello.j\Desktop\Working\Proposal to CFO.pptx`

**Explanation:**
Run Zimmerman tool lnkcmd on recent folder

![Proof](./screenshots/Task 3.png)
---

### Task 4
**Question:** The threat actor discovered a privilege that allows specific volume-level management operations and could be exploited to get full control over the C drive. What is this special privilege?

**Answer:** `SeManageVolumePrivilege`

**Explanation:**


> *Screenshot placeholder*
---

### Task 5
**Question:** What is the name of the executable downloaded by the threat actor to exploit previously found privilege?

**Answer:** `SeManageVolumeExploit.exe`

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** What is the full URL from where the threat actor tried to download a DLL file?

**Answer:** `http://freehackingtool.com/tools/PrintConfig.dll`

**Explanation:**
Reviewing the Chromes browser downloads

> *Screenshot placeholder*
---

### Task 7
**Question:** The malicious DLL file was not successfully downloaded, as the download was interrupted by the safe browsing safety feature. Research Browser forensics and find the description of the interrupt reason that caused the download to be disrupted.

**Answer:** `The user shut down the browser`

**Explanation:**
review the interrup_reason which is 41

![Proof](./screenshots/Task 7.png)
---

### Task 8
**Question:** Since the download was not successful from the browser directly, which LOLBIN did the threat actor use to download this file successfully?

**Answer:** `certutil.exe`

**Explanation:**
Upon reviewing the logs

> *Screenshot placeholder*
---

### Task 9
**Question:** When was the malicious DLL file successfully downloaded using this LOLBIN?

**Answer:** `2025-05-28 12:45:37`

**Explanation:**
review the usnjrnl logs to get download time based on creation time

![Proof](./screenshots/Task 9_11)
---

### Task 10
**Question:** To gain System privileges, the threat actor replaced an existing DLL with the same name. What is the original path of the legitimate DLL?

**Answer:** `C:\Windows|System32\spool\drivers\x64\3\Printconfig.dll`

**Explanation:**


> *Screenshot placeholder*
---

### Task 11
**Question:** The threat actor removed the legitimate DLL before replacing it with the malicious DLL. When was the legit DLL deleted?

**Answer:** `2025-05-28 12:47:06`

**Explanation:**
Review UsnJrnl look for deleted actions

> *Screenshot placeholder*
---

### Task 12
**Question:** When was the malicious DLL detected as malware?

**Answer:** `2025-05-28 15:19:35`

**Explanation:**
Review windows defender logs. Filter for mailicous dll and you should be able to find information for next few questions

![Proof](./screenshots/Task 12_13_14_15.png)
---

### Task 13
**Question:** The threat actor initiated a Windows component to load this DLL. What is the CLSID of this component?

**Answer:** `{854A20FB-2D44-457D-992F-EF13785D2B51}`

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** What is the name of the service/object associated with this CLSID?

**Answer:** `PrintNotify`

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** What is the SHA1 hash of the malicious DLL file?

**Answer:** `916564984e38f8bb91921cd4e40b64156a72142b`

**Explanation:**


> *Screenshot placeholder*
---

### Task 16
**Question:** A Second DLL file was downloaded from the same malicious domain. Where was it downloaded on the filesystem?

**Answer:** `C:\windows\system32\wbem\tzres.dll`

**Explanation:**
Parse MFT and filter for similar time and observe the results

![Proof](./screenshots/Task 16_17.png)
---

### Task 17
**Question:** When was this DLL downloaded on the system?

**Answer:** `2025-05-28 12:54:23`

**Explanation:**


> *Screenshot placeholder*
---

### Task 18
**Question:** The threat actor downloaded a VBScript for command execution to facilitate the DLL execution of the second malicious DLL. What is the full path of this script after it was moved to a new location?

**Answer:** `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\a.vbs`

**Explanation:**
Review MFT logs. We originally notices a.vbs in browser downlaod history

> *Screenshot placeholder*
---

### Task 19
**Question:** What is the full command that the script is configured to execute?

**Answer:** `cmd.exe /c systeminfo`

**Explanation:**


> *Screenshot placeholder*
---

### Task 20
**Question:** The threat actor configured the VBS script to be hidden from the Windows GUI (File Explorer). When was this attribute set on the file?

**Answer:** `2025-05-28 12:56:11`

**Explanation:**


> *Screenshot placeholder*
---

### Task 21
**Question:** Which process loads the previously identified DLL with this command? The command executed by the VBS script ultimately facilitates loading and execution of the Second malicious DLL, providing persistence and execution capabilities to the attacker.

**Answer:** `wmiprvse.exe`

**Explanation:**


> *Screenshot placeholder*
---

### Task 22
**Question:** The threat actor downloaded an image file to change the desktop wallpaper. What is the full path of this file?

**Answer:** `C:\Users\Public\Pictures\gg.tmp`

**Explanation:**
Review Powershell commandline logs

![Proof](./screenshots/Task 23.png)
---

### Task 23
**Question:** The threat actor then proceeded to change the desktop wallpaper of the compromised user to the newly downloaded image. Find the time when the wallpaper was altered?

**Answer:** `2025-05-28 15:04:41`

**Explanation:**
review event logs 4688 or powershell logs

> *Screenshot placeholder*
---

### Task 24
**Question:** When did the victim user log in to their workstation after the compromise?

**Answer:** `2025-05-28 15:04:41`

**Explanation:**
Check 4624 logsfor otello.j after the change of wallpaper 

> *Screenshot placeholder*
---

### Task 25
**Question:** What is the message on the new wallpaper?

**Answer:** `HACKED BY ANARCHY`

**Explanation:**
Use autospy to review CryptchaceURL

> *Screenshot placeholder*
---

