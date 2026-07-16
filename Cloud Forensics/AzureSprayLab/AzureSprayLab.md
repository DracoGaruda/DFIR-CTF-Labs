# DFIR Report: AzureSprayLab

| Metadata | Details |
|----------|---------|
| **Date** | 2025-12-21 |
| **Platform** | Azure |
| **Tasks** | 18 |

## 1. Scenario

A mid-sized technology company called Compliant Secure, with 50 employees, has recently migrated to Microsoft 365. During a routine security review, the SOC team discovered suspicious authentication patterns.

As a SOC analyst, you've been tasked with investigating these authentication anomalies, implementing detection mechanisms, and hardening the Azure AD environment against

## 2. DFIR Analysis Summary

On June 29, 2025, a targeted password spray attack originating from German IP addresses struck the "Compliant Secure" Azure AD environment, impacting 89 unique user accounts and generating significant volumes of 50126 (invalid credentials) and 50053 (Smart Lockout) errors. Leveraging Microsoft Sentinel analytics with specific authentication thresholds, we traced the activity to a cluster of IPs—most notably 3.123.15.9—and successfully isolated a single compromised account, louisa.hartis@compliantsecure.store, amidst the noise of failed attempts. The incident response protocol necessitated immediate session revocation via the revokeSignInSessions Graph API.

## 3. Challenge Solutions

### Task 1
**Question:** During the initial investigation, you notice a pattern of failed authentication attempts. What is the most common Result Type associated with password spray attacks in Azure AD sign-in logs?

**Answer:** `50126`

**Explanation:** Just review the sign-in alerts

---

### Task 2
**Question:** Analyzing the sign-in logs, you identify multiple source IP addresses attempting authentication. Which IP address had the highest number of failed login attempts during the attack window?

**Answer:** `3.123.15.9`

**Explanation:** Filter logs based on aggregate fr the count

> <img width="1412" height="728" alt="Q2" src="https://github.com/user-attachments/assets/a471e0b7-23e0-41f9-94f8-94fe7906940e" />

---

### Task 3
**Question:** The attacker appears to be using a specific user agent string across all spray attempts. What is the user agent string identified in the attack?

**Answer:** `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36`

**Explanation:** review user agent field

> <img width="1672" height="591" alt="Q3" src="https://github.com/user-attachments/assets/65d2c355-103e-4457-9936-bd2d66436a78" />

---

### Task 4
**Question:** Smart Lockout events are crucial for identifying password spray victims. What is the specific sign-in error code that indicates an account has been locked out by Azure AD Smart Lockout?

**Answer:** `50053`

**Explanation:** filte for the error ids

> <img width="1592" height="755" alt="Q4" src="https://github.com/user-attachments/assets/f1438413-8c09-4726-893d-442c0c53b8ec" />

---

### Task 5
**Question:** What time (UTC) in CreatedDateTime did the password spray attack begin based on the first failed authentication attempt?

**Answer:** `6/29/2025, 6:35:06`

**Explanation:** filter with creation date time coloumn

---

### Task 6
**Question:** How many unique user accounts in the Compliant Secure company were targeted in this password spray attack?

**Answer:** `89`

**Explanation:** filter by the result type 50126 and aggregate user principal name by count


> <img width="1483" height="1051" alt="Q6" src="https://github.com/user-attachments/assets/dc6fd181-2d52-425a-9e47-9ce79e21d63f" />

---

### Task 7
**Question:** The attack originated from a single country. What is the name of the region where the attack originated?

**Answer:** `DE`

**Explanation:** Review LocationDetails

> <img width="1372" height="863" alt="Q7" src="https://github.com/user-attachments/assets/e7c1fe12-8a21-4a22-be61-b6625689803e" />

---

### Task 8
**Question:** In Microsoft Sentinel, navigate to Content Hub and install the Microsoft Entra ID solution. Once installed, go to Analytics > Rule templates and you'll see several analytics rules related to password spray attacks. What is the name of the analytics rule that identifies evidence of failures from multiple accounts against Microsoft Entra ID applications?

**Answer:** `Password spray attack against Microsoft Entra ID application`

---

### Task 9
**Question:** In the rule configuration, there's a parameter called authenticationThreshold that defines how many failed account attempts from a single IP address trigger an alert. Based on the attack patterns observed in this incident, what is the maximum value you should set for authenticationThreshold to ensure the rule would have detected this specific attack?

**Answer:** `3`

**Explanation:** From erlier logs review different ips have  failed account logs

---

### Task 10
**Question:** Review the KQL query in your analytics rule and locate the parameter that defines the time window for grouping authentication attempts. What is the value (in minutes) set for the authenticationWindow parameter?

**Answer:** `20`

**Explanation:** Just review the kql query for the authentication window


> <img width="1089" height="393" alt="Q10" src="https://github.com/user-attachments/assets/599f36a5-17cb-46f4-8c5c-780b887f5f0b" />

---

### Task 11
**Question:** Navigate to Incidents in Microsoft Sentinel and open the newly created incident. Review the entities section, which shows all IP addresses involved in this attack. List all attacker IP addresses identified in the incident.

**Answer:** `3.123.14.162, 3.123.14.126, 3.70.195.178`

> <img width="1276" height="1119" alt="Q11" src="https://github.com/user-attachments/assets/c5bc8dba-c4de-4945-b71a-698aa0768b1e" />

---

### Task 12
**Question:** What is the minimum number of failed attempts from a single IP before Smart Lockout triggers for an unfamiliar location (based on default settings)?

**Answer:** `10`

> <img width="1059" height="405" alt="Q12" src="https://github.com/user-attachments/assets/f08475d0-8737-476b-a9b0-fd368bd887d4" />

---

### Task 13
**Question:** Investigation revealed that despite the widespread attack, only one account was successfully compromised. What is the user principal name of the account that was successfully breached?

**Answer:** `louisa.hartis@compliantsecure.store`

**Explanation:** filter for successfull logons 

> <img width="1667" height="1121" alt="Q13" src="https://github.com/user-attachments/assets/741b61f9-d6b2-425d-9ede-f8fc5a367808" />

---

### Task 14
**Question:** What Conditional Access policy would have prevented 99% of this password spray attack according to Microsoft's research?

**Answer:** `Block Legacy Authentication:`

**Explanation:** As password spray often uses older protocols (IMAP, POP, SMTP) that bypass MFA. A CA policy can block these entirely for most users, stopping the attack at the first step.

---

### Task 15
**Question:** When implementing Azure AD Password Protection to prevent compromised accounts, what is the maximum number of password entries you can add to the custom banned password list?

**Answer:** `1000`

---

### Task 16
**Question:** For federated environments, what Windows Server 2019 feature provides similar protection to Azure AD Smart Lockout?

**Answer:** `Extranet Smart Lockout`

---

### Task 17
**Question:** In your custom analytics rule configuration, navigate to the "Automated response" tab where you can attach playbooks. If you were to create a playbook that revokes all active sessions for compromised users detected by this rule, what Microsoft Graph API method would the playbook use to invalidate all user sessions?

**Answer:** `revokeSignInSessions`

---

### Task 18
**Question:** According to NIST guidelines referenced in the mitigation section, what is the recommended minimum password length for modern password policies?

**Answer:** `8`

---








