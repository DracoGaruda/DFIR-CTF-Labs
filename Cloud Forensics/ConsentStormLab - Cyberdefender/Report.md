# DFIR Report: ConsentStorm Lab

| Metadata | Details |
|----------|---------|
| **Date** | 2026-02-18 |
| **Platform** | Azure |
| **Tasks** | 25 |

## 1. Scenario



## 2. DFIR Summary


## 3. Challenge Solutions

### Task 1
**Question:** What is the email address of the attacker in the initial phishing email?

**Answer:** `david@nexgenenrgy.com`

**Explanation:**


> *Screenshot placeholder*
---

### Task 2
**Question:** What is the display name of the malicious OAuth application that the user granted consent to, and how many permissions were requested?

**Answer:** `BudgetPlannerApp, 5`

**Explanation:**


> *Screenshot placeholder*
---

### Task 3
**Question:** After gaining initial access, how many phishing emails did the attacker send from the compromised account?

**Answer:** `3`

**Explanation:**


> *Screenshot placeholder*
---

### Task 4
**Question:** What is the name of the malicious document that was uploaded to SharePoint?

**Answer:** `Immediate_Review.doc`

**Explanation:**


> *Screenshot placeholder*
---

### Task 5
**Question:** The attacker enumerated the compromised user's OneDrive files and discovered a PowerShell script containing credentials. What is the name of this script?

**Answer:** `Provisioning-Script.ps1`

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** What is the attacker's first IP address used in this attack, and from which country does this IP originate?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** The attacker enumerated Azure resource groups using the service account whose credentials were discovered in the victim's OneDrive script. How many resource groups were successfully enumerated, and how many were blocked due to access restrictions?

**Answer:** `2,2`

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** Which resources were blocked by ABAC restrictions?

**Answer:** `RG-FinanceCore, kv-financecore`

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** The attacker explored the Automation Account to find credentials. What is the name of the Automation Account that was accessed?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** What is the name of the second service account that the attacker compromised using the credentials discovered in the runbook?

**Answer:** `svc-automation@nexgenenergy.com`

**Explanation:**


> *Screenshot placeholder*
---

### Task 11
**Question:** After bypassing ABAC restrictions, the attacker accessed the Key Vault and retrieved a secret. What is the name of the secret that was retrieved?

**Answer:** `jessica-turner-cred`

**Explanation:**


> *Screenshot placeholder*
---

### Task 12
**Question:** The attacker used the credentials from the Key Vault to authenticate as a high-privilege account. What is the user principal name of this account?

**Answer:** `jessica.turner@nexgenenergy.com`

**Explanation:**


> *Screenshot placeholder*
---

### Task 13
**Question:** The second service account added a new client secret to the BudgetPlannerApp to maintain persistent access. What is the Key ID of this secret?

**Answer:** `0309ccc7-c9ea-4b95-a8ee-e886b6c25422`

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** The high-privilege account created a time-limited credential for another user account. At what time was this credential created? (Hint: ActivityDateTime)

**Answer:** `01/21/2026 04:56:50`

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** The first service account was added to a high-privilege group to escalate privileges. What group was the account added to, and when did this group membership modification occur?

**Answer:** `Finance-Operations, 01/21/2026 03:48:00`

**Explanation:**


> *Screenshot placeholder*
---

### Task 16
**Question:** To bypass ABAC restrictions, the attacker modified a resource tag. What is the tag key and value that was added to the resource?

**Answer:** `CostCenter, FIN001`

**Explanation:**


> *Screenshot placeholder*
---

### Task 17
**Question:** What is the second IP address used by the attacker during the final phase of the attack?

**Answer:** `176.31.90.129`

**Explanation:**


> *Screenshot placeholder*
---

### Task 18
**Question:** Using the temporary access pass, the attacker authenticated as the final target account. What is the name of the first file that was accessed?

**Answer:** `Investor-Presentation-2026.pptx`

**Explanation:**


> *Screenshot placeholder*
---

### Task 19
**Question:** How many files in total were accessed by the attacker on the final target account?

**Answer:** `7`

**Explanation:**


> *Screenshot placeholder*
---

### Task 20
**Question:** Based on the IOCs (Indicators of Compromise) identified in this investigation, what threat actor group is responsible for this attack?

**Answer:** `STORM-0558`

**Explanation:**


> *Screenshot placeholder*
---

### Task 21
**Question:** What is the MITRE ATT&CK technique ID for the 'Illicit Consent Grant' attack pattern used in the initial compromise phase?

**Answer:** `T1528`

**Explanation:**


> *Screenshot placeholder*
---

### Task 22
**Question:** What is the MITRE ATT&CK technique ID for the 'Persistence' phase where the attacker created a Temporary Access Pass?

**Answer:** `T1556`

**Explanation:**


> *Screenshot placeholder*
---

### Task 23
**Question:** What is the operation name recorded in the AzureDiagnostics logs when a secret is successfully retrieved from a Key Vault?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 24
**Question:** What authentication control, if enabled on the initial compromised user's account, would have prevented the attacker from granting consent to the malicious application?

**Answer:** `Do not allow user consent`

**Explanation:**


> *Screenshot placeholder*
---

### Task 25
**Question:** What is the maximum validity period (in hours) for a Temporary Access Pass created in Azure AD?

**Answer:** `8`

**Explanation:**


> *Screenshot placeholder*
---

