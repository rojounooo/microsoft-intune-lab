# Runbook — Outlook Keeps Asking to Sign In

## Scenario
A user's Outlook keeps prompting them to sign in repeatedly, even after entering the correct password. It accepts the password but prompts again within minutes.

---

## Steps

### 1. Rule Out a Service Outage
[admin.microsoft.com](https://admin.microsoft.com) → **Health** → **Service health** — check for active incidents affecting Exchange Online or Entra ID authentication.

### 2. Check if Others Are Affected
Ask colleagues or check the helpdesk queue. If multiple users are affected it is a tenant-wide issue — escalate immediately rather than troubleshooting the individual device.

### 3. Check Device Compliance
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device → check compliance status.

A non-compliant device can trigger Conditional Access to force re-authentication on every sign in. If non-compliant, resolve the compliance issue and force a sync.

### 4. Check Password Expiry
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → confirm the password has not expired.

If expired, reset via M365 Admin Centre and communicate the temp password securely.

### 5. Check Sign-In Logs for Errors
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Sign-in logs**

Look for repeated failed or interrupted sign-in attempts and note any error codes. These will identify whether the issue is authentication, Conditional Access, or token related.

### 6. Clear the Credential Cache (Token Cache Fix)
A corrupted authentication token stored locally in Outlook is a common cause of repeated sign-in prompts.

1. Close Outlook completely
2. Open **Credential Manager** in Windows (search in Start)
3. Click **Windows Credentials**
4. Remove any entries related to Microsoft Office, Outlook, or MicrosoftOffice
5. Restart Outlook and sign in fresh

This forces a clean authentication and resolves the loop in many cases.

### 7. Sign Out and Back Into Outlook
If clearing credentials does not resolve it:
1. In Outlook go to **File** → **Office Account** → **Sign out**
2. Close Outlook
3. Reopen Outlook and sign back in

---

## Escalate If
- Multiple users are affected — escalate immediately, likely a tenant-wide issue
- Sign-in logs show a Conditional Access block — escalate to 2nd line to review the policy
- Clearing credentials and re-signing in does not resolve the issue — escalate to 2nd line
- Suspected Modern Authentication misconfiguration — escalate to 2nd line or IT admin

---

## Notes
- Clearing the Windows Credential Manager cache resolves this issue more often than expected — try it before anything more complex
- Always check sign-in logs for error codes before escalating — they tell you exactly what is failing and save 2nd line time
- Repeated sign-in prompts after a password change are normal for a few minutes while cached tokens expire — ask the user how long it has been happening before treating it as an issue
