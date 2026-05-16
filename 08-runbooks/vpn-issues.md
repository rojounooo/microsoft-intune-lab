# Runbook — VPN Not Connecting

## Scenario
A user working from home cannot connect to the company VPN. They were connecting fine last week and have not made any changes.

---

## Steps

### 1. Rule Out a Wider Outage
Before troubleshooting the individual device, check with colleagues or the infrastructure team whether the VPN service is up. If the VPN server is down it affects everyone — do not spend time troubleshooting the device.

### 2. Check Basic Connectivity
Ask the user:
- Are you connected to your home WiFi?
- Can you open a website in your browser?

If they cannot reach the internet at all, the issue is their home network — not the VPN. Ask them to restart their router and try again.

### 3. Ask for the Error Message
The error message in the VPN client identifies the cause quickly. Common errors:

| Error | Likely cause |
|---|---|
| Authentication failed | Credentials or MFA issue |
| Connection timed out | VPN server issue or ISP blocking the port |
| Client won't open | VPN software issue |
| Certificate error | Client certificate expired |

### 4. Check Password Expiry
If the error is authentication related, check whether the user's password has expired since last week:

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Sign-in logs** — look for failed authentication attempts

If expired, reset the password via M365 Admin Centre and communicate the temp password securely.

### 5. Check MFA
If the VPN uses MFA, confirm the user's MFA registration is still valid — particularly if they have recently changed phones.

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Authentication methods**

### 6. Check Device Compliance
If Conditional Access is configured to require a compliant device for VPN access, a non-compliant device will be blocked.

[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device → check compliance status.

If non-compliant, resolve the failing settings and force a sync.

### 7. Try Restarting the VPN Client
Ask the user to:
1. Close the VPN client completely
2. Restart the device
3. Try connecting again

### 8. Reinstall the VPN Client
If the client is throwing errors or will not open, try reinstalling it via Company Portal if it was deployed through Intune.

---

## Escalate If
- The VPN server appears to be down — escalate to the infrastructure or network team immediately
- Certificate expiry is suspected — escalate to 2nd line for certificate renewal
- The issue persists after password reset, compliance fix, and VPN client restart — escalate to 2nd line
- The user's ISP may be blocking the VPN port — escalate to 2nd line to advise on alternative connection methods

---

## Notes
- Always rule out a server-side or wider outage first — do not spend time on a device that is working correctly
- Password expiry is a common cause of VPN authentication failures for remote workers who do not get the expiry prompt as prominently as office-based staff
- Some ISPs throttle or block VPN traffic — if the user can connect on a different network (e.g. mobile hotspot) the issue is their ISP, not the device
