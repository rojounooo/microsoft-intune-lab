# Runbook — MFA Prompting Repeatedly

## Scenario
A user is being prompted for MFA every time they sign in, even though they have already set it up. The repeated prompts started recently.

---

## Steps

### 1. Rule Out a Service Outage
Check [admin.microsoft.com](https://admin.microsoft.com) → **Health** → **Service health** for any active incidents affecting Entra ID or authentication services.

### 2. Check Device Compliance
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device → check compliance status.

A non-compliant device can trigger Conditional Access to force re-authentication on every sign in. If non-compliant, resolve the compliance issue first.

### 3. Ask About Recent Changes
- Has the user set up a new phone recently?
- Did they reinstall or restore their authenticator app from a backup?
- Has their phone's time and date changed?

Any of these can break the existing MFA registration.

### 4. Check MFA Registration in Entra ID
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Authentication methods**

Confirm:
- An authenticator app is registered
- There are no duplicate or outdated registrations (e.g. an old phone still listed)

### 5. Check the Authenticator App
Ask the user to open their authenticator app and confirm:
- The work account is listed
- The code is refreshing every 30 seconds
- Their phone's date and time is set to **automatic** — TOTP codes are time-based and will fail if the clock is off

### 6. Reset MFA Registration if Required
If the registration is missing, broken, or the user has a new phone:

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Authentication methods** → **Require re-register MFA**

- Delete any old authentication methods from the same page before issuing the re-register prompt
- Stay on the call and walk the user through scanning the QR code with their authenticator app
- Confirm they can successfully approve an MFA prompt before ending the call

---

## Escalate If
- Compliance is fine and MFA registration looks correct but the issue persists — escalate to 2nd line
- Multiple users are affected — likely a Conditional Access policy change or tenant-wide issue, escalate immediately
- Suspected Conditional Access misconfiguration — escalate to 2nd line

---

## Notes
- Phone time and date being set to manual rather than automatic is a surprisingly common cause of TOTP failures — always check this
- Always remove old authentication methods before issuing a re-register prompt to avoid confusion
- Never end the call before confirming the new MFA registration is working
