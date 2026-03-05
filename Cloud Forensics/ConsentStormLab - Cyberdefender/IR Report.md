# DFIR Report: ConsentStorm Lab - CyberDefenders

## 📝 Case Overview
* **Platform:** [CyberDefenders](https://cyberdefenders.org)
* **Case:** ConsentStorm
* **Date:** 2026-02-18
* **Category:** Cloud Forensics (Azure / Entra ID)
* **Investigator:** Sid (GCFE, GREM, GCFA)

---

## 1. Scenario
On January 21, 2026, the SOC at NexGen Energy detected suspicious activity within their Microsoft Entra ID and Azure environment. The attack chain was initiated via a phishing email, leading to an **Illicit OAuth Consent Grant**. The adversary successfully escalated privileges, bypassed **Attribute-Based Access Control (ABAC)**, and exfiltrated sensitive financial data.

---

## 2. Executive Summary
This investigation identifies the threat actor **STORM-0558** as the party responsible for the breach. The attacker leveraged a "living-off-the-cloud" strategy, using legitimate Azure features like Automation Accounts, Resource Tags, and Temporary Access Passes (TAP) to move laterally and maintain persistence.

---

## 3. Technical Analysis

### Phase 1: Initial Access & Persistence
The compromise began when a user interacted with a phishing email from `david@nexgenenrgy.com` (a typo-squatted domain). 
* **Technique:** Illicit Consent Grant (**MITRE T1528**).
* **Malicious App:** `BudgetPlannerApp`.
* **Permissions:** The user granted **5 permissions**, giving the attacker programmatic access to the mailbox and OneDrive.
* **Attacker IP:** `51.89.156.153` (China).

### Phase 2: Internal Reconnaissance
The attacker used the compromised account to send **3 internal phishing emails** and uploaded `Immediate_Review.doc` to SharePoint to facilitate further lateral movement. While searching OneDrive, the attacker discovered `Provisioning-Script.ps1`, which contained hardcoded service account credentials.

### Phase 3: Lateral Movement & ABAC Bypass
The attacker attempted to access protected Resource Groups but was initially blocked by ABAC restrictions.
1.  **Credential Harvesting:** The attacker accessed an **Azure Automation Account** and retrieved credentials for `svc-automation@nexgenenergy.com` from a runbook.
2.  **Resource Manipulation:** To bypass ABAC, the attacker modified the resource tag for the Key Vault to `CostCenter: FIN001`.
3.  **Privilege Escalation:** By satisfying the tag requirement, the attacker accessed **Azure Key Vault** and performed a `SecretGet` operation to retrieve `jessica-turner-cred`.

### Phase 4: Persistence & Exfiltration
* **Account Takeover:** Authenticated as `jessica.turner@nexgenenergy.com`.
* **Persistence:** A new client secret (`0309ccc7-c9ea-4b95-a8ee-e886b6c25422`) was added to the malicious app.
* **Exfiltration:** A **Temporary Access Pass (TAP)** was created for the target account. The attacker accessed **7 files** in total, including `Investor-Presentation-2026.pptx`.
* **Secondary Attacker IP:** `176.31.90.129`.

---

## 4. Indicators of Compromise (IOCs)

| Type | Value | Description |
| :--- | :--- | :--- |
| **IP Address** | `51.89.156.153` | Initial Access IP (China) |
| **IP Address** | `176.31.90.129` | Final Phase / Exfiltration IP |
| **Domain** | `nexgenenrgy.com` | Phishing / Spoofed Domain |
| **File Name** | `Provisioning-Script.ps1` | Script containing leaked credentials |
| **File Name** | `Immediate_Review.doc` | Malicious Document on SharePoint |
| **App Name** | `BudgetPlannerApp` | Malicious OAuth Application |
| **Key ID** | `0309ccc7-c9ea-4b95-a8ee-e886b6c25422` | Rogue Client Secret for Persistence |

---

## 5. MITRE ATT&CK Mapping

* **Initial Access:** T1566.003 (Phishing: Malicious Service)
* **Credential Access:** T1528 (Steal Application Access Token)
* **Persistence:** T1098.003 (Account Manipulation: Token Exchange)
* **Defense Evasion:** T1550 (Use Alternate Authentication Material)
* **Privilege Escalation:** T1098 (Account Manipulation)

---

## 6. Recommendations

1.  **Disable User Consent:** Configure Entra ID to require **Admin Consent** for all applications to prevent unauthorized OAuth grants.
2.  **Secure Secrets:** Eliminate hardcoded credentials in scripts and runbooks. Transition to **Azure Managed Identities**.
3.  **Tag Governance:** Restrict the `Microsoft.Resources/tags/write` permission. In an ABAC environment, the ability to edit tags is equivalent to the ability to modify permissions.
4.  **Monitor TAPs:** Implement alerting for the `New-MgUserTemporaryAccessPass` operation in Azure Audit logs.

---
*Created for portfolio purposes based on CyberDefenders lab completion.*
