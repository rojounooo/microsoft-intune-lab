# Runbook — Full Device Onboarding

## Scenario
A new employee is starting. HR have provided their details. No account or device has been set up yet.

---

## Steps

### 1. Confirm Details with HR
Before creating anything, confirm the following with HR:
- Full name
- Job title and department
- Manager
- Start date
- Whether they are receiving a company device or using their own (BYOD)
- Any specific systems or shared mailboxes they need access to

### 2. Create the User Account
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → **All users** → **New user**

| Field | Value |
|---|---|
| **Display name** | Employee's full name |
| **Username** | Follow the organisation's naming convention e.g. `firstname.lastname@domain.com` |
| **Job title** | From HR details |
| **Department** | From HR details |
| **Manager** | Set from HR details |

Note the temporary password.

### 3. Assign Licences
[admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the new user → **Licenses and apps** → assign:
- Microsoft 365 (appropriate tier for their role)
- Microsoft Intune

### 4. Assign to Entra ID Groups
[entra.microsoft.com](https://entra.microsoft.com) → **Groups** → add the user to:
- Their department group
- Any role-specific groups that determine app and policy assignments
- Any relevant distribution lists for team emails

### 5. Grant Shared Mailbox Access (if required)
If their role requires access to a shared mailbox:
[admin.microsoft.com](https://admin.microsoft.com) → **Teams & groups** → **Shared mailboxes** → select the mailbox → **Members** → add the user

The shared mailbox will appear automatically in their Outlook.

### 6. Set Up the Device

**Company device — Autopilot:**
If the device's hardware hash is pre-registered in Intune and an Autopilot deployment profile is assigned, the device will self-configure when the user turns it on and signs in with their work account.

**Company device — Manual enrolment:**
1. Complete Windows setup using a local administrator account
2. **Settings** → **Accounts** → **Access work or school** → **Connect** → **Join this device to Microsoft Entra ID**
3. Sign in with the new user's account
4. Install Company Portal from the Microsoft Store
5. Sign in to Company Portal and follow the enrolment prompts
6. Confirm the device appears in Intune → **Devices** → **All devices**

**BYOD:**
1. Ask the user to install Company Portal on their personal device
2. Walk them through signing in and enrolling
3. Explain what Intune can and cannot see on their personal device — Intune manages company apps and data only, not personal content

### 7. Verify Compliance
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → confirm the device shows as **Compliant**

### 8. Communicate to HR and the User
Provide HR with:
- The new user's username
- Temporary password
- Instructions for the user to change their password on first sign in and who to call if they have issues

---

## Escalate If
- Licence assignment requires admin access you do not have — raise a request
- Shared mailbox access requires permissions above your level — escalate to 2nd line
- Autopilot does not trigger correctly — escalate to 2nd line

---

## Notes
- Always set the manager field in Entra ID — it is used for approval workflows and org charts
- Check for shared mailbox requirements before the user's first day — it is easy to miss and causes frustration on day one
- For BYOD users, be transparent about what Intune manages — users often assume IT has full access to their personal device
- Username conventions must be consistent — check what format the organisation uses before creating the account
