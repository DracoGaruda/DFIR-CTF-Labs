# Incident Response Report: RogueAzureLab

**Date:** December 22, 2025  
**Investigator:** Sid  
**Case Status:** Closed  
**Machine/Lab Name:** RogueAzureLab (Hack The Box)  

---

## 1. Scenario Context
On November 14, 2025, security monitoring detected suspicious authentication activity in the Azure tenant. Anomalous sign-in patterns were observed from multiple geographic locations. Automated alerts flagged unauthorized administrative actions and configuration changes shortly thereafter. 

**Scope of Investigation:**
* Azure Sign-in Logs (Interactive and Non-Interactive)
* Azure Audit Logs (Role assignments and App registrations)
* Azure Storage Access Logs (Blob activity)

---

## 2. Executive Summary
The investigation confirmed a successful **Password Spray** attack against the `compliantsecure.store` tenant. The threat actor compromised one account, transitioned to a secondary infrastructure in Singapore to evade detection, and established multiple persistence mechanisms. The attack culminated in the unauthorized elevation of a second user to Global Administrator and the exfiltration of sensitive company data.

---

## 3. Incident Timeline (UTC)
| Time | Source IP | Action | Details |
| :--- | :--- | :--- | :--- |
| 14:22:05 | 52.59.240.166 | **Initial Access** | Successful login for `mharmon@compliantsecure.store` |
| 14:35:12 | 52.221.180.165 | **Infrastructure Pivot** | Pivot to Singapore IP using Linux-based browser |
| 14:42:00 | 52.221.180.165 | **Persistence** | Registered App: `OfficeRead` |
| 14:45:30 | 52.221.180.165 | **Persistence** | Registered App: `VaultApp` |
| 14:58:10 | 52.221.180.165 | **Privilege Escalation** | Assigned Global Admin role to `lwilliams@compliantsecure.store` |
| 15:15:45 | 52.221.180.165 | **Exfiltration** | Downloaded `Confidintal.png` from `mainstoragestore01` |

---

## 4. Technical Analysis

### 4.1 Initial Access & Compromise
Analysis of interactive sign-in logs identified a targeted password spray campaign originating from **52.59.240.166** (Germany). The attacker targeted multiple users, including `max harmon` and `logan williams`. 
* **Primary Compromise:** The account `mharmon@compliantsecure.store` was successfully accessed at approximately 14:22 UTC.

### 4.2 Post-Exploitation & Pivot
Following the breach, the actor shifted to a secondary infrastructure IP **52.221.180.165** (Singapore). The logs indicate a change in the environment to a Linux workstation, suggesting the attacker was utilizing a specialized attack platform for the remainder of the operation.

### 4.3 Persistence & Administrative Backdoors
The attacker performed two primary actions to ensure continued access to the tenant:
1. **Malicious App Registration:** Two applications, **"OfficeRead"** and **"VaultApp"**, were registered. These are common TTPs used to maintain access via OAuth tokens even if the compromised user's password is changed.
2. **Account Escalation:** The attacker used the compromised admin session to grant the **Global Administrator** role to `lwilliams@compliantsecure.store`, creating a redundant high-privilege backdoor.

### 4.4 Data Exfiltration
The actor accessed the **`mainstoragestore01`** storage account. Storage blob logs confirm that the Singapore-based IP successfully executed a `GetBlob` command.
* **Exfiltrated File:** `Confidintal.png`

---

## 5. Indicators of Compromise (IOCs)
| Type | Value | Description |
| :--- | :--- | :--- |
| **IP Address** | `52.59.240.166` | Attacker Infrastructure (Initial Access/DE) |
| **IP Address** | `52.221.180.165` | Attacker Infrastructure (Post-Exploitation/SG) |
| **User Account** | `mharmon@compliantsecure.store` | Compromised Source Account |
| **User Account** | `lwilliams@compliantsecure.store` | Escalated Backdoor Account |
| **Azure App** | `OfficeRead` | Malicious Persistence Mechanism |
| **Azure App** | `VaultApp` | Malicious Persistence Mechanism |

---

## 6. Remediation Recommendations
1. **Immediate Revocation:** Revoke all refresh tokens for `mharmon` and `lwilliams`.
2. **Privilege Cleanup:** Remove the Global Administrator role from `lwilliams` and delete the `OfficeRead` and `VaultApp` application registrations.
3. **MFA Enforcement:** Implement Conditional Access policies requiring MFA for all administrative roles to prevent future password spray success.
4. **Monitoring:** Configure alerts for any new "Global Administrator" role assignments or application registrations containing high-privilege Graph API permissions.
