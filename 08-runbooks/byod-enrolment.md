# Runbook — User Does Not Want to Enrol Personal Device

## Scenario
A user is being repeatedly prompted to enrol their personal device every time they open Outlook. They do not want to enrol their personal device but need access to work email.

---

## Steps

### 1. Check the Organisation's BYOD Policy
Before responding to the user, confirm what the organisation's policy actually allows. Your response depends entirely on this:
- **Enrolment required for any device accessing email** — the user must enrol or use a different device. Non-negotiable.
- **MAM without enrolment supported** — Outlook can be managed without full device enrolment. This is the ideal resolution for users who do not want to enrol.
- **Personal devices not supported** — the user must use their company device. Escalate to their manager if they do not have one.

### 2. Explain What Enrolment Does and Does Not Do
Many users refuse enrolment because they believe IT will have full access to their personal device. Clarify:

**What Intune can see and manage on an enrolled personal device:**
- Company apps and data managed by Intune
- Device compliance status (OS version, encryption, passcode)

**What Intune cannot see:**
- Personal photos, messages, emails, or apps
- Browsing history
- Personal data outside of managed apps

Being transparent about this often resolves the objection.

### 3. If MAM Without Enrolment is Supported
Mobile Application Management (MAM) allows Intune to manage just the Outlook app without enrolling the device. The user installs Outlook, signs in, and Intune applies a policy to that app only — such as requiring a PIN to open Outlook and preventing copy/paste to personal apps.

Walk the user through:
1. Installing Outlook from the App Store or Google Play
2. Signing in with their work account
3. Completing any app protection policy prompts (PIN setup etc)

No full device enrolment is required.

### 4. If Enrolment is Required by Policy
Explain to the user that enrolment is a requirement for accessing company resources from a personal device, and offer the alternatives:
- Use their company device instead
- Access email via [outlook.office.com](https://outlook.office.com) in a mobile browser — no enrolment required, though functionality may be limited
- Request a company device — escalate to their manager and HR

### 5. Temporary Access via Outlook Online
While the situation is being resolved, direct the user to [outlook.office.com](https://outlook.office.com) in a browser for temporary access to email.

---

## Escalate If
- The organisation's BYOD policy is unclear — escalate to your manager for clarification before advising the user
- The user needs a company device — escalate to their manager and HR
- MAM configuration is not working correctly — escalate to 2nd line

---

## Notes
- Never advise workarounds that contradict the organisation's BYOD policy — clarify the policy first
- Transparency about what Intune can and cannot see resolves most objections — most users assume full surveillance
- MAM without enrolment is the ideal middle ground for BYOD users and is worth knowing about even if not currently configured
