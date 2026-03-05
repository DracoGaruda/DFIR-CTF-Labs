# DFIR Report: ConsentStorm Lab

| Metadata | Details |
|----------|---------|
| **Date** | 2026-02-18 |
| **Platform** | Azure |
| **Tasks** | 25 |

## 1. Scenario

On January 21, 2026, the Security Operations Center (SOC) at NexGen Energy received alerts indicating suspicious activity within their Microsoft Entra ID and Azure environment.

The incident appears to have started when an employee in the Finance department received what looked like a legitimate email from a colleague. After interacting with the email, unusual OAuth consent activity and unauthorized access patterns were detected across multiple accounts and Azure resources.

Initial triage suggests the attacker gained access to sensitive cloud resources, pivoted through multiple accounts, and potentially accessed confidential financial data. Threat intelligence indicates the TTPs may be associated with a known APT group.

Your task is to investigate the full scope of this breach, trace the attacker's movements, and document the techniques used throughout the attack chain.

## 2. DFIR Summary


## 3. Challenge Solutions

### Task 1
**Question:** What is the email address of the attacker in the initial phishing email?

**Answer:** `david@nexgenenrgy.com`

**Explanation:**


> <img width="930" height="963" alt="Q1" src="https://github.com/user-attachments/assets/6f10596b-5b9e-488a-acbb-77448f76ee9a" />

---

### Task 2
**Question:** What is the display name of the malicious OAuth application that the user granted consent to, and how many permissions were requested?

**Answer:** `BudgetPlannerApp, 5`

**Explanation:**


> <img width="738" height="833" alt="Q2" src="https://github.com/user-attachments/assets/a8b879b3-87eb-4d34-b78e-fb27ca0689e4" />

---

### Task 3
**Question:** After gaining initial access, how many phishing emails did the attacker send from the compromised account?

**Answer:** `3`

**Explanation:**


> <img width="1012" height="358" alt="Q3" src="https://github.com/user-attachments/assets/dee7f8e8-3dee-44ee-94f8-90aee5ffe701" />

---

### Task 4
**Question:** What is the name of the malicious document that was uploaded to SharePoint?

**Answer:** `Immediate_Review.doc`

**Explanation:**


> <img width="934" height="1017" alt="Q4" src="https://github.com/user-attachments/assets/6ee6e864-4486-43c8-b1fd-6e6943aa7abc" />

---

### Task 5
**Question:** The attacker enumerated the compromised user's OneDrive files and discovered a PowerShell script containing credentials. What is the name of this script?

**Answer:** `Provisioning-Script.ps1`

**Explanation:**


> <img width="656" height="490" alt="Q5" src="https://github.com/user-attachments/assets/55d87048-3d88-4e54-9e33-706fb827c23f" />

---

### Task 6
**Question:** What is the attacker's first IP address used in this attack, and from which country does this IP originate?

**Answer:** `51.89.156.153, China`

**Explanation:**


> <img width="1165" height="583" alt="Q6" src="https://github.com/user-attachments/assets/ffcc31b5-a705-454e-a029-ced32f3a885f" />

---

### Task 7
**Question:** The attacker enumerated Azure resource groups using the service account whose credentials were discovered in the victim's OneDrive script. How many resource groups were successfully enumerated, and how many were blocked due to access restrictions?

**Answer:** `2,2`

**Explanation:**


> <img width="663" height="434" alt="Q7_1" src="https://github.com/user-attachments/assets/39cd5175-f010-477c-a744-58a4266b7577" />

<img width="530" height="325" alt="Q7_2" src="https://github.com/user-attachments/assets/f00c193c-04cd-415e-9a18-14ad4a4499c1" />


---

### Task 8
**Question:** Which resources were blocked by ABAC restrictions?

**Answer:** `RG-FinanceCore, kv-financecore`

**Explanation:**


> <img width="513" height="322" alt="Q8" src="https://github.com/user-attachments/assets/d79c763e-6f4b-41cd-ad59-2c3855ae3121" />

---

### Task 9
**Question:** The attacker explored the Automation Account to find credentials. What is the name of the Automation Account that was accessed?

**Answer:** ``

**Explanation:**


> <img width="1204" height="990" alt="Q9_10" src="https://github.com/user-attachments/assets/42cfcc4d-f662-4ea0-8ed6-e8fd9f6162ad" />

---

### Task 10
**Question:** What is the name of the second service account that the attacker compromised using the credentials discovered in the runbook?

**Answer:** `svc-automation@nexgenenergy.com`

---

### Task 11
**Question:** After bypassing ABAC restrictions, the attacker accessed the Key Vault and retrieved a secret. What is the name of the secret that was retrieved?

**Answer:** `jessica-turner-cred`

**Explanation:**


> <img width="683" height="390" alt="Q11" src="https://github.com/user-attachments/assets/73faa169-7c07-4213-bbd6-831ff811a982" />

---

### Task 12
**Question:** The attacker used the credentials from the Key Vault to authenticate as a high-privilege account. What is the user principal name of this account?

**Answer:** `jessica.turner@nexgenenergy.com`

**Explanation:**

---

### Task 13
**Question:** The second service account added a new client secret to the BudgetPlannerApp to maintain persistent access. What is the Key ID of this secret?

**Answer:** `0309ccc7-c9ea-4b95-a8ee-e886b6c25422`

**Explanation:**


> <img width="991" height="993" alt="Q13" src="https://github.com/user-attachments/assets/444d53b1-b269-411e-90ed-d84f7306d5b5" />

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


> <img width="1210" height="523" alt="Q14" src="https://github.com/user-attachments/assets/52f84df3-2629-426d-8f97-34a2cdcd4bd8" />

---

### Task 16
**Question:** To bypass ABAC restrictions, the attacker modified a resource tag. What is the tag key and value that was added to the resource?

**Answer:** `CostCenter, FIN001`

**Explanation:**


> <img width="1210" height="523" alt="Q14" src="https://github.com/user-attachments/assets/3630dc91-37f2-49af-9001-e6f47400c874" />

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

---

### Task 21
**Question:** What is the MITRE ATT&CK technique ID for the 'Illicit Consent Grant' attack pattern used in the initial compromise phase?

**Answer:** `T1528`

---

### Task 22
**Question:** What is the MITRE ATT&CK technique ID for the 'Persistence' phase where the attacker created a Temporary Access Pass?

**Answer:** `T1556`

---

### Task 23
**Question:** What is the operation name recorded in the AzureDiagnostics logs when a secret is successfully retrieved from a Key Vault?

**Answer:** `SecretGet`

---

### Task 24
**Question:** What authentication control, if enabled on the initial compromised user's account, would have prevented the attacker from granting consent to the malicious application?

**Answer:** `Do not allow user consent`

**Explanation:** only authorized users should be able to grant concent to applications

---

### Task 25
**Question:** What is the maximum validity period (in hours) for a Temporary Access Pass created in Azure AD?

**Answer:** `8`

**Explanation:** Default maximum validity period is 8 hours

---



