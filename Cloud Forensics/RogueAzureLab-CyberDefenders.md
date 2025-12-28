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

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 2
**Question:** After numerous failed attempts, the attacker successfully gained access to an account. What is the username of the first account that was compromised?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 3
**Question:** Following the initial compromise, the attacker began using a new infrastructure for post-exploitation activities. What is the second IP address used by the attacker?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 4
**Question:** From which country did the successful sign-in originate when the attacker pivoted to their secondary infrastructure for post-exploitation activities?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
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

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** What highly privileged role was assigned to the second user account to grant it administrative control over the tenant?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** The attacker's final objective was data exfiltration. They targeted a specific storage resource to access sensitive files. What is the name of the storage account they accessed?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** The attacker successfully downloaded a sensitive file from the storage account. What is the name of the exfiltrated file?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---


