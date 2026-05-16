# Runbook — User Has Incorrect Access to Colleague's Files

## Scenario
A user calls to report they can see files on a shared network drive that belong to a colleague and that they should not have access to. They have not opened or modified any files.

---

## Steps

### 1. Acknowledge the Report
Thank the user for reporting it rather than ignoring it or accessing the files. This is exactly the right behaviour and should be noted in the ticket.

### 2. Document Everything Before Taking Action
Before making any changes, document:
- Exactly what the user can see and should not have access to
- The path of the shared drive or folder
- When they first noticed the access
- Whether anyone else is aware of the issue

Do not change permissions immediately — doing so destroys the audit trail needed for investigation and any potential breach report.

### 3. Identify How the Access Was Granted
The cause may not always be a group membership issue. Check the following:

- Was the user added to the wrong Entra ID group directly?
- Was a group granted access to the wrong drive or folder?
- Were the shared drive permissions misconfigured directly rather than via a group?
- Did a recent onboarding or offboarding change have unintended side effects?

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Groups** — review group memberships for anything unexpected.

[entra.microsoft.com](https://entra.microsoft.com) → **Groups** → check the groups that have access to the shared drive — confirm membership is correct.

### 4. Escalate to 2nd Line and the Security Team
Permissions changes on shared drives are typically above 1st line. Escalate with all documented details:
- What the user can access and should not be able to
- How the access appears to have been granted
- The timeline of when it was noticed

The security team need to assess whether this constitutes a data breach — if the files contain personal or sensitive data, GDPR reporting obligations may apply even if the files were not opened.

### 5. Reassure the User
Confirm you are investigating, thank them again for reporting it, and let them know what happens next. Do not leave the user without a response.

---

## Escalate If
- The files contain personal, sensitive, or confidential data — escalate to the security team immediately, GDPR obligations may apply
- The misconfiguration appears to affect multiple users — escalate urgently
- A recent offboarding or onboarding change appears to have caused the issue — escalate to whoever made the change

---

## Notes
- Never change permissions before documenting and escalating — the audit trail is critical for any breach investigation
- Accidental access to files is still a potential data breach under GDPR, even if the files were not opened — always escalate to the security team to assess
- Thank users who report this kind of issue — it reflects good security awareness and should be encouraged
- The most common cause is a group membership error following an onboarding or offboarding process — check recent changes to group memberships in the Entra ID audit logs
