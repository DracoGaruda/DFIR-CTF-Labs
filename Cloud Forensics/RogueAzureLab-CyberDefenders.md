# DFIR Report: RogueAzureLab

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-22 |
| **Platform** | Azure |
| **Tasks** | 10 |

## 1. Scenario

On November 14, 2025, security monitoring detected suspicious authentication activity in the Azure tenant, with anomalous sign-in patterns from multiple geographic locations. Shortly after, automated alerts flagged unauthorized administrative actions and configuration changes within the environment.

You have been provided with Azure sign-in logs, audit logs, and storage access logs from the affected tenant. Your mission is to investigate the incident, determine how the attacker gained initial access, identify what persistence mechanisms were established, document any privilege changes, and confirm whether sensitive data was accessed or exfiltrated

## 2. Summary


## 3. Challenge Solutions

### Task 1
**Question:** The investigation begins by analyzing a password spray attack that targeted several users in the primary tenant. What IP address did the attacker originate the password spray attack from?

**Answer:** `52.59.240.166`

**Explanation:** Review interactive Signin Logs and filter for failed authentictions. You can find multiple logon attemepts targetting users "max harmon" and "logan williams" that were failures followed by a successfull one.


> <img width="1678" height="1138" alt="Q1" src="https://github.com/user-attachments/assets/50546c14-20ec-4ea6-8174-a61edf7bfcb3" />

---

### Task 2
**Question:** After numerous failed attempts, the attacker successfully gained access to an account. What is the username of the first account that was compromised?

**Answer:** `mharmon@compliantsecure.store`

**Explanation:** The one successfull logon from above ip address gives the information that attacker was sucessfull with max harmon account


> <img width="1622" height="1126" alt="Q2" src="https://github.com/user-attachments/assets/6b778b9d-0ede-448a-91c2-4abcb0ad6ba1" />

---

### Task 3
**Question:** Following the initial compromise, the attacker began using a new infrastructure for post-exploitation activities. What is the second IP address used by the attacker?

**Answer:** `52.221.180.165`

**Explanation:**review signin logs and look for successfull logons for max hermon. on review you find two difeerent ips one form germany and one from singapore. One from singapore uses linux


> <img width="1645" height="1141" alt="Q3" src="https://github.com/user-attachments/assets/afe803f4-2884-479d-9730-fe3d56d5eae9" />

---

### Task 4
**Question:** From which country did the successful sign-in originate when the attacker pivoted to their secondary infrastructure for post-exploitation activities?

**Answer:** `Singapore`

---

### Task 5
**Question:** To establish persistence, the attacker registered malicious applications. What is the name of the first application they created?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** The attacker created a second application to ensure persistent access, this one intended to access directory information. What is the name of this second application?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** To create a redundant backdoor, the attacker used the compromised administrator account to elevate the privileges of another user. What is the User Principal Name of the account that had its privileges escalated?

**Answer:** `lwilliams@compliantsecure.store`

**Explanation:** Review audit logs for role assignemnet and filter for malicious second IP you end up finding following log.


> <img width="1274" height="610" alt="Q7" src="https://github.com/user-attachments/assets/97822783-df1d-44b8-8519-7cd16e44bc9c" />

---

### Task 8
**Question:** What highly privileged role was assigned to the second user account to grant it administrative control over the tenant?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** The attacker's final objective was data exfiltration. They targeted a specific storage resource to access sensitive files. What is the name of the storage account they accessed?

**Answer:** `mainstoragestore01`

**Explanation:** Review blob Storage logs. As you can find mainstoragestore01 only storage in logs


> <img width="1274" height="610" alt="Q7" src="https://github.com/user-attachments/assets/314910ef-0e99-450c-87ce-0323007cd7be" />

---

### Task 10
**Question:** The attacker successfully downloaded a sensitive file from the storage account. What is the name of the exfiltrated file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---



