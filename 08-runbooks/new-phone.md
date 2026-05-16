# Runbook — New Phone, Cannot Access Work Email

## Scenario
A user has set up a new phone and can no longer access their work email. They were accessing it fine on their old phone.

---

## Steps

### 1. Identify How They Were Accessing Email
Ask the user:
- Are they using the **Outlook app** or the built-in mail app?
- Were they using Company Portal on their old phone?

The resolution differs depending on how they were set up.

### 2. Check MFA Registration
The most common cause is a broken MFA registration. The authenticator app does not transfer to a new phone automatically.

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Authentication methods**

- Are there authentication methods listed for the old phone?
- Is there a valid registration for the new phone?

### 3. Reset MFA Registration
1. Delete any old authentication methods from the **Authentication methods** page
2. Click **Require re-register MFA**
3. Stay on the call and walk the user through:
   - Installing their authenticator app on the new phone (Aegis, Microsoft Authenticator etc)
   - Scanning the QR code presented at next sign in
   - Approving a test MFA prompt to confirm it works
4. Confirm MFA is working before ending the call

### 4. Reinstall Outlook on the New Phone
If the user was accessing email via Outlook:
1. Install Outlook from the App Store or Google Play on the new phone
2. Sign in with their work account
3. Approve the MFA prompt using the newly registered authenticator
4. Confirm email is loading

### 5. Check Company Portal (BYOD)
If the user's old phone was enrolled in Intune via Company Portal, the new phone will need to be enrolled too:
1. Install Company Portal from the App Store or Google Play
2. Sign in and follow the enrolment prompts
3. Confirm the new device appears in [intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices**

### 6. Retire the Old Device from Intune
Once the new phone is enrolled, retire the old one:

[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the old device → **Retire**

---

## Escalate If
- MFA re-registration is not resolving the issue — escalate to 2nd line
- The user's account appears locked or blocked — escalate
- Company Portal enrolment fails on the new phone — check licensing and escalate if unresolved

---

## Notes
- MFA registrations do not transfer between phones — this is by design and is a security feature, not a fault
- Always remove old authentication methods before issuing a re-register prompt — leaving old entries causes confusion
- If the user had a managed Outlook app on their old phone, Intune may have applied MAM policies to it — these will need to be re-applied on the new phone through re-enrolment or re-signing into Outlook
