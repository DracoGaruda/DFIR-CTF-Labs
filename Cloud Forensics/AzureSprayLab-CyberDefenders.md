# DFIR Report: AzureSprayLab

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-27 |
| **Platform** | Azure |
| **Tasks** | 18 |

## 1. Executive Summary
*Summary of the incident goes here.*

## 2. Timeline
| Timestamp | Event |
|-----------|-------|
|           |       |

## 3. Challenge Solutions

### Task 1
**Question:** During the initial investigation, you notice a pattern of failed authentication attempts. What is the most common Result Type associated with password spray attacks in Azure AD sign-in logs?

**Answer:** `50126`

**Explanation:**
Just review the sign-in alerts

> *Screenshot placeholder*
---

### Task 2
**Question:** Analyzing the sign-in logs, you identify multiple source IP addresses attempting authentication. Which IP address had the highest number of failed login attempts during the attack window?

**Answer:** `3.123.15.9`

**Explanation:**
Filter logs based on aggregate fr the count

> *Screenshot placeholder*
---

### Task 3
**Question:** The attacker appears to be using a specific user agent string across all spray attempts. What is the user agent string identified in the attack?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 4
**Question:** Smart Lockout events are crucial for identifying password spray victims. What is the specific sign-in error code that indicates an account has been locked out by Azure AD Smart Lockout?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 5
**Question:** What time (UTC) in CreatedDateTime did the password spray attack begin based on the first failed authentication attempt?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 6
**Question:** How many unique user accounts in the Compliant Secure company were targeted in this password spray attack?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 7
**Question:** The attack originated from a single country. What is the name of the region where the attack originated?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 8
**Question:** In Microsoft Sentinel, navigate to Content Hub and install the Microsoft Entra ID solution. Once installed, go to Analytics > Rule templates and you'll see several analytics rules related to password spray attacks. What is the name of the analytics rule that identifies evidence of failures from multiple accounts against Microsoft Entra ID applications?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 9
**Question:** In the rule configuration, there's a parameter called authenticationThreshold that defines how many failed account attempts from a single IP address trigger an alert. Based on the attack patterns observed in this incident, what is the maximum value you should set for authenticationThreshold to ensure the rule would have detected this specific attack?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 10
**Question:** Review the KQL query in your analytics rule and locate the parameter that defines the time window for grouping authentication attempts. What is the value (in minutes) set for the authenticationWindow parameter?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 11
**Question:** Navigate to Incidents in Microsoft Sentinel and open the newly created incident. Review the entities section, which shows all IP addresses involved in this attack. List all attacker IP addresses identified in the incident.

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 12
**Question:** What is the minimum number of failed attempts from a single IP before Smart Lockout triggers for an unfamiliar location (based on default settings)?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 13
**Question:** Investigation revealed that despite the widespread attack, only one account was successfully compromised. What is the user principal name of the account that was successfully breached?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 14
**Question:** What Conditional Access policy would have prevented 99% of this password spray attack according to Microsoft's research?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 15
**Question:** When implementing Azure AD Password Protection to prevent compromised accounts, what is the maximum number of password entries you can add to the custom banned password list?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 16
**Question:** For federated environments, what Windows Server 2019 feature provides similar protection to Azure AD Smart Lockout?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 17
**Question:** In your custom analytics rule configuration, navigate to the "Automated response" tab where you can attach playbooks. If you were to create a playbook that revokes all active sessions for compromised users detected by this rule, what Microsoft Graph API method would the playbook use to invalidate all user sessions?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

### Task 18
**Question:** According to NIST guidelines referenced in the mitigation section, what is the recommended minimum password length for modern password policies?

**Answer:** ``

**Explanation:**


> *Screenshot placeholder*
---

