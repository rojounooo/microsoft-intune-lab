# Runbook — Cannot Access Email or Teams

## Scenario
A user cannot access their work email or Microsoft Teams. They were working fine previously and have not made any changes.

---

## Steps

### 1. Rule Out a Service Outage
Before troubleshooting the individual device, check the Microsoft 365 Service Health dashboard:
[admin.microsoft.com](https://admin.microsoft.com) → **Health** → **Service health**

If there is an active incident affecting Exchange or Teams, the issue is not with the user's device. Inform the user and advise them to check back once Microsoft resolves the incident.

### 2. Check Connectivity
Ask the user:
- Are you connected to WiFi?
- Can you open a website in your browser?

If they are not connected to the internet, the issue is connectivity — not an account or device issue.

### 3. Check Online Versions
Ask the user to try accessing [outlook.office.com](https://outlook.office.com) and [teams.microsoft.com](https://teams.microsoft.com) in a browser.

- If online versions work but desktop apps do not — the issue is with the app, not the account
- If online versions also fail — the issue is with the account or licence

### 4. Check Account Status
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → confirm:
- Account is not disabled
- Sign-in is not blocked

### 5. Check Licence
[admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the user → **Licenses and apps** → confirm Microsoft 365 and Intune licences are assigned.

### 6. Check Password Expiry
If the password has expired the user will be unable to authenticate. Reset via M365 Admin Centre and communicate the temporary password securely.

### 7. Check Device Compliance
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device → check compliance status and last check-in time.

If non-compliant, identify the failing setting and resolve it. Force a sync after fixing.

### 8. Force a Sync
On the user's device: **Settings** → **Accounts** → **Access work or school** → click the work account → **Info** → **Sync**

---

## Escalate If
- Service Health shows no active incident but multiple users are affected — escalate to 2nd line
- Licence has been removed — escalate to IT admin or 2nd line for licence reassignment
- Account is disabled and you do not have authority to re-enable — escalate to 2nd line

---

## Notes
- Always check for a service outage first — do not spend time troubleshooting a device issue that does not exist
- Password expiry is a common cause — check the expiry date in Entra ID if the user cannot recall when they last changed it
