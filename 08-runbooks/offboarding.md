# Runbook — Employee Offboarding

## Scenario
HR have confirmed an employee has left the company. The manager has requested that the former employee's access is removed and their device is dealt with.

---

## Steps

### 1. Confirm the Leaver with HR
Before taking any action, confirm the offboarding request has come from or been verified by HR. Do not action offboarding requests from managers alone without HR confirmation.

### 2. Revoke Active Sessions
Immediately terminate any active authenticated sessions:

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Revoke sessions**

### 3. Disable the Account
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Edit properties** → **Settings** → set **Block sign in** to **Yes**

> If you do not have authority to disable accounts, escalate to 2nd line immediately — this is the highest priority step.

### 4. Action the Device

**Company-owned device:**
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device

- If the device is being returned and reused → **Retire** — removes company data and policies, leaves the device intact for re-enrolment
- If the device is being decommissioned → **Wipe** — full factory reset

**Personal device (BYOD):**
- Use **Retire** only — removes company data and unenrols the device without touching personal content
- Never wipe a personal device

> If the device is offline and does not respond to the command, document it and flag to the security team.

### 5. Remove Licences
[admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the user → **Licenses and apps** → remove all assigned licences

> Licence removal is typically handled by IT admin or 2nd line. Raise a request if you do not have access.

### 6. Remove Group Memberships
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Groups** → remove from all groups

### 7. Handle Shared Mailboxes and Distribution Lists
Remove the user from any shared mailboxes or distribution lists they had access to. Confirm with the manager whether their emails need to be forwarded to someone else during the transition period.

### 8. Communicate to Manager and HR
Confirm all actions taken in writing to the manager and HR. Include timestamps.

### 9. Document and Close the Ticket
Record all actions taken, by whom, and at what time. Retain for audit purposes.

---

## Escalate If
- You do not have authority to disable the account — escalate immediately, this is the priority action
- The data on the device may be sensitive or constitute a reportable breach — escalate to the security team
- Licence removal requires admin access you do not have — raise a request to 2nd line

---

## Notes
- Revoke sessions before disabling the account — disabling alone does not immediately terminate active sessions
- Always confirm with HR before actioning — do not rely solely on a manager's request
- For BYOD devices, always use Retire not Wipe — wiping a personal device is a serious issue
- Document everything with timestamps — offboarding records may be needed for audit or legal purposes
