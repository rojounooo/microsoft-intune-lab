# Runbook — Stolen Device

## Scenario
A user reports their company laptop has been stolen. They are calling from their personal phone.

---

## Steps

### 1. Verify Identity
The user cannot verify identity via their device. Use knowledge-based questions:
- Employee ID number
- Date of birth
- Manager's name

### 2. Reset the User's Password
Immediately reset the account password to prevent the thief from accessing company services using cached credentials.

[admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the user → **Reset password**

### 3. Revoke Active Sessions
Disabling the account or resetting the password alone does not immediately terminate active sessions. Revoke all active sessions:

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Revoke sessions**

### 4. Lock or Wipe the Device in Intune
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device

- **Remote lock** — locks the screen immediately. Use if the device may be recovered
- **Wipe** — factory resets the device. Use if the device is confirmed stolen and will not be recovered

> Follow your organisation's policy on when to lock vs wipe. In most cases a confirmed theft warrants an immediate wipe.

> The device must be connected to the internet to receive the command. If offline, the command will queue and execute when it next connects.

### 5. Escalate to Manager and Security Team
A stolen device is a potential data breach. Escalate immediately:
- Inform your manager
- Notify the security team — GDPR reporting obligations may apply depending on what data was on the device

### 6. Advise the User
- File a police report and obtain a crime reference number — required for insurance
- Contact HR regarding a replacement device

### 7. Document Everything
Record the time the theft was reported, all actions taken, and by whom. This timeline is critical if a data breach report is required.

---

## Escalate If
- You do not have authority to wipe the device — escalate to 2nd line or manager for approval
- The data on the device may constitute a reportable breach — escalate to the security team immediately
- Account disable is required — escalate to 2nd line if you do not have the authority

---

## Notes
- Always revoke sessions in addition to resetting the password — resetting the password alone does not terminate existing authenticated sessions
- A stolen device is a security incident first and a support ticket second — escalate early
- Timestamp every action taken in the ticket
