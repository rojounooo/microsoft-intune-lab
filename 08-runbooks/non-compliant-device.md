# Runbook — Device Non-Compliant, User Has Urgent Meeting

## Scenario
A user's screen is showing a message saying their device is not compliant and they need to contact IT. They have an important meeting in 10 minutes.

---

## Steps

### 1. Get the User Into Their Meeting First
Do not attempt to resolve the compliance issue before addressing the immediate urgency. Ask the user:
- Do you have a phone or another device you can use?
- Can you join the meeting via [teams.microsoft.com](https://teams.microsoft.com) in a browser on another device?

Get them into their meeting first. The compliance issue can be resolved while they are in the meeting or immediately after.

### 2. Identify the Compliance Failure
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device → **Device compliance**

Note all failing settings.

### 3. Resolve the Compliance Issue
Common causes and fixes:

| Failing setting | Fix |
|---|---|
| BitLocker | Enable BitLocker on the device — search Manage BitLocker in Start |
| Firewall | Re-enable Windows Firewall via Windows Security |
| Password complexity | Reset password to meet policy requirements |
| Antivirus / Defender | Re-enable Defender via Windows Security |
| OS version | Check Windows Update and install pending updates |

### 4. Force a Sync
After resolving the failing settings, force a sync:

**Settings** → **Accounts** → **Access work or school** → click the work account → **Info** → **Sync**

Allow 5-10 minutes for the compliance status to update in Intune.

### 5. Confirm Compliance
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → confirm the device shows as **Compliant**

---

## Escalate If
- The compliance issue cannot be resolved quickly — escalate to 2nd line
- The failing setting requires admin intervention on the device — escalate
- You are considering removing the device from the compliance policy — do not do this without manager approval. Exempting a device from compliance creates a security gap and requires authorisation

---

## Notes
- Always get the user into their meeting first via an alternative device — urgency should not push you into making security decisions above your authority
- Do not remove devices from compliance policies to resolve an urgent issue — this is a security decision, not a support decision, and requires authorisation
- A compliant device that suddenly goes non-compliant is worth investigating after the immediate issue is resolved — check what changed
