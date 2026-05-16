# Runbook — Device Restarted Unexpectedly, Unsaved Work Lost

## Scenario
A user calls frustrated after their device automatically restarted and they lost unsaved work. They want to know why it happened and how to prevent it.

---

## Steps

### 1. Acknowledge the Frustration
Losing unsaved work is genuinely disruptive. Acknowledge it before moving into troubleshooting — do not immediately jump to asking questions.

### 2. Check Intune Audit Logs
Confirm whether a remote restart was triggered by IT:

[intune.microsoft.com](https://intune.microsoft.com) → **Tenant administration** → **Audit logs**

Filter by the device name and look for any restart actions triggered around the time the user reported the issue.

### 3. Check Windows Update History
The most common cause of unexpected restarts on a managed device is a Windows Update installing and triggering a reboot.

Ask the user to:
1. **Settings** → **Windows Update** → **Update history**
2. Check whether an update installed around the time of the restart

### 4. Check Intune Windows Update Rings
If a Windows Update ring is configured in Intune, confirm its restart settings:

[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **Configuration** → open the Update ring policy → check **Restart settings**

If no active hours are configured, the device may restart at any time once updates are installed.

### 5. Explain to the User
Inform the user that:
- Updates are managed centrally by IT and restarts are sometimes unavoidable
- They should receive a notification before a forced restart occurs — if they did not, note this and investigate
- Saving work regularly and not leaving unsaved work unattended when updates are pending will prevent data loss in future

### 6. Raise a Policy Improvement if Active Hours Are Not Configured
If the Intune Update ring does not have active hours configured, raise this with 2nd line as a policy improvement. Active hours prevent forced restarts during working hours:

**Devices** → **Configuration** → Update ring → **Active hours** — set to cover the organisation's working hours (e.g. 08:00–18:00)

---

## Escalate If
- The restart was not caused by Windows Update and no IT-triggered action is in the audit logs — escalate to 2nd line to investigate the restart reason further via Event Viewer
- Active hours are not configured on the Update ring — raise with 2nd line as a policy improvement
- The user lost significant work and requires data recovery — escalate to 2nd line

---

## Notes
- Windows Update is the most common cause of unexpected restarts on managed devices — always check Update history first
- Intune audit logs confirm whether a remote restart was triggered by IT — check this before assuming it was an update
- Active hours in the Windows Update ring prevent restarts during working hours and should be configured on all managed devices — if missing, flag it
- Encourage users to save work regularly regardless of update schedules
