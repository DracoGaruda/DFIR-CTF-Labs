# DFIR Report: WorkFromHome

| Metadata | Details |
|----------|---------|
| **Date** | 2025-11-17 |
| **Platform** | Windows |
| **Tasks** | 25 |

## 1. Scenario

Wowza Enterprise (Wowza Inc.) has hired you to investigate an incident involving a workstation used by Otello John, which is believed to have been compromised by a threat actor. The attacker reportedly changed the desktop wallpaper to a questionable image. The IT team has already provided you with initial information, and it is your duty to report back your findings.

## 2. DFIR Summary

The investigation reveals a targeted intrusion beginning on May 27, 2025, where a threat actor gained initial access to the otello.j workstation via a credential-harvesting phishing link (login.wowzalnc.co.th) and subsequent RDP connection. Once inside, the attacker conducted reconnaissance, accessing sensitive corporate documents and identifying the SeManageVolumePrivilege, which they exploited by leveraging the certutil.exe LOLBin to bypass browser defenses and download a malicious PrintConfig.dll. This file was used to replace the legitimate system driver, allowing the attacker to escalate to System privileges via the PrintNotify service. Persistence was established by deploying a hidden VBScript (a.vbs) in the Startup folder that utilized WMI (wmiprvse.exe) to load a secondary malicious payload (tzres.dll), culminating in the defacement of the victim's desktop with the message "HACKED BY ANARCHY" on May 28, 2025.

## 3. Challenge Solutions

### Task 1
**Question:** Identify the phishing URL that the user clicked on, resulting in credential harvesting

**Answer:** `http://login.wowzalnc.co.th/logon.php`

**Explanation:** Check the Chrome browser downloads

> <img width="1571" height="143" alt="Task 1" src="https://github.com/user-attachments/assets/bcad8cee-68a0-413b-8539-c590d3b96686" />
---

### Task 2
**Question:** When did the threat actor gain access to the victim's computer via RDP for the first time?

**Answer:** `2025-05-27 11:59:57`

**Explanation:** Check in 4624 logs for logon type 10

> <img width="1113" height="664" alt="Task 2" src="https://github.com/user-attachments/assets/0725c801-3bd8-411b-8073-c681f5b327e3" />
---

### Task 3
**Question:** The threat actor accessed several sensitive files on the victim's work-related folder. What is the full path of the PowerPoint presentation file opened by the attacker?

**Answer:** `C:\Users\otello.j\Desktop\Working\Proposal to CFO.pptx`

**Explanation:** Run Zimmerman tool lnkcmd on recent folder

> <img width="1898" height="220" alt="Task 3" src="https://github.com/user-attachments/assets/f5735508-8953-4b47-9b6b-38c7a423eb70" />
---

### Task 4
**Question:** The threat actor discovered a privilege that allows specific volume-level management operations and could be exploited to get full control over the C drive. What is this special privilege?

**Answer:** `SeManageVolumePrivilege`

---

### Task 5
**Question:** What is the name of the executable downloaded by the threat actor to exploit previously found privilege?

**Answer:** `SeManageVolumeExploit.exe`

---

### Task 6
**Question:** What is the full URL from where the threat actor tried to download a DLL file?

**Answer:** `http://freehackingtool.com/tools/PrintConfig.dll`

**Explanation:** Reviewing the Chromes browser downloads

---

### Task 7
**Question:** The malicious DLL file was not successfully downloaded, as the download was interrupted by the safe browsing safety feature. Research Browser forensics and find the description of the interrupt reason that caused the download to be disrupted.

**Answer:** `The user shut down the browser`

**Explanation:** review the interrup_reason which is 41

> <img width="1597" height="192" alt="Task 7" src="https://github.com/user-attachments/assets/05234709-9f4c-47c1-8af8-fca9f799d6e8" />
---

### Task 8
**Question:** Since the download was not successful from the browser directly, which LOLBIN did the threat actor use to download this file successfully?

**Answer:** `certutil.exe`

**Explanation:** Upon reviewing the logs

---

### Task 9
**Question:** When was the malicious DLL file successfully downloaded using this LOLBIN?

**Answer:** `2025-05-28 12:45:37`

**Explanation:** Review the usnjrnl logs to get download time based on creation time

><img width="1854" height="565" alt="Task 9_11" src="https://github.com/user-attachments/assets/f3d7a634-00b8-40b1-b64a-58b15d334485" />

---

### Task 10
**Question:** To gain System privileges, the threat actor replaced an existing DLL with the same name. What is the original path of the legitimate DLL?

**Answer:** `C:\Windows|System32\spool\drivers\x64\3\Printconfig.dll`

**Explanation:** By filtering for printconfig.dll we can find the original dll filepath in $MFT logs

---

### Task 11
**Question:** The threat actor removed the legitimate DLL before replacing it with the malicious DLL. When was the legit DLL deleted?

**Answer:** `2025-05-28 12:47:06`

**Explanation:** Review UsnJrnl look for deleted actions

---

### Task 12
**Question:** When was the malicious DLL detected as malware?

**Answer:** `2025-05-28 15:19:35`

**Explanation:** Review windows defender logs. Filter for mailicous dll and you should be able to find information for next few questions

> <img width="1411" height="367" alt="Task 12_!3_!4_!5" src="https://github.com/user-attachments/assets/b2b1e33e-99a1-4a1b-8b7f-5ffd79cfabbd" />
---

### Task 13
**Question:** The threat actor initiated a Windows component to load this DLL. What is the CLSID of this component?

**Answer:** `{854A20FB-2D44-457D-992F-EF13785D2B51}`

**Explanation:** CLSID is provided with each detection

---

### Task 14
**Question:** What is the name of the service/object associated with this CLSID?

**Answer:** `PrintNotify`

**Explanation:** The detection points out service being exploited

---

### Task 15
**Question:** What is the SHA1 hash of the malicious DLL file?

**Answer:** `916564984e38f8bb91921cd4e40b64156a72142b`

**Explanation:** Sha1 file is provided within the windows defender logsfor the associated detection

---

### Task 16
**Question:** A Second DLL file was downloaded from the same malicious domain. Where was it downloaded on the filesystem?

**Answer:** `C:\windows\system32\wbem\tzres.dll`

**Explanation:** Parse MFT and filter for similar time and observe the results

> <img width="1890" height="82" alt="Task 16_17" src="https://github.com/user-attachments/assets/8690253d-496d-4cf1-954e-40381d893b22" />
---

### Task 17
**Question:** When was this DLL downloaded on the system?

**Answer:** `2025-05-28 12:54:23`

**Explanation:** Timestamp is found in the above finding

---

### Task 18
**Question:** The threat actor downloaded a VBScript for command execution to facilitate the DLL execution of the second malicious DLL. What is the full path of this script after it was moved to a new location?

**Answer:** `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\a.vbs`

**Explanation:** Review MFT logs. We originally noticed a.vbs in browser downlaod history

> <img width="1902" height="451" alt="task18" src="https://github.com/user-attachments/assets/d3bacb89-213a-40ef-b8c5-f03f1af50c53" />
---

### Task 19
**Question:** What is the full command that the script is configured to execute?

**Answer:** `cmd.exe /c systeminfo`

**Explanation:** review Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt


> <img width="632" height="124" alt="Task19" src="https://github.com/user-attachments/assets/7d56d608-30a1-49c0-853a-65dc7cd36a67" />
---

### Task 20
**Question:** The threat actor configured the VBS script to be hidden from the Windows GUI (File Explorer). When was this attribute set on the file?

**Answer:** `2025-05-28 12:56:11`

---

### Task 21
**Question:** Which process loads the previously identified DLL with this command? The command executed by the VBS script ultimately facilitates loading and execution of the Second malicious DLL, providing persistence and execution capabilities to the attacker.

**Answer:** `wmiprvse.exe`

**Explanation:** reviewing wmi logs would provide this information

---

### Task 22
**Question:** The threat actor downloaded an image file to change the desktop wallpaper. What is the full path of this file?

**Answer:** `C:\Users\Public\Pictures\gg.tmp`

**Explanation:** Review Powershell commandline logs

---

### Task 23
**Question:** The threat actor then proceeded to change the desktop wallpaper of the compromised user to the newly downloaded image. Find the time when the wallpaper was altered?

**Answer:** `2025-05-28 15:04:41`

**Explanation:** review event logs 4688 or powershell logs

> <img width="876" height="111" alt="Task 23" src="https://github.com/user-attachments/assets/96a1f807-a4b6-4c9e-867b-0e69f94aa345" />
---

### Task 24
**Question:** When did the victim user log in to their workstation after the compromise?

**Answer:** `2025-05-28 15:04:41`

**Explanation:** Check 4624 logsfor otello.j after the change of wallpaper 

> <img width="1285" height="665" alt="Task 24" src="https://github.com/user-attachments/assets/54f792b7-2322-4c4d-9c1c-0252fb22cd51" />
---

### Task 25
**Question:** What is the message on the new wallpaper?

**Answer:** `HACKED BY ANARCHY`

**Explanation:** Use autospy to review CryptchaceURL

---



