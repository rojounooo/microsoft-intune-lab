# Runbook — Suspected Phishing Email

## Scenario
A user has received an email appearing to be from the IT department asking them to click a link and enter their Microsoft credentials urgently. They have not clicked it yet and want to verify if it is legitimate.

---

## Steps

### 1. Confirm Immediately — Did IT Send It?
Check the IT shared mailbox sent items to confirm whether the email came from your team.

If it did not come from IT, confirm to the user it is a phishing attempt and instruct them:
- Do not click any links
- Do not open any attachments
- Do not forward the email to colleagues

### 2. Verify the Sender Address
Ask the user to check the actual email address, not just the display name. Phishing emails often display a legitimate-looking name such as "IT Support" while the actual address is a spoofed or unrelated domain.

Common red flags:
- Domain does not match the organisation (e.g. `@company-support.com` instead of `@company.com`)
- Random characters in the address
- Slightly misspelled domain (e.g. `c0mpany.com`)

### 3. Advise the User to Report the Email
In Outlook, the user can report the email directly:
- **Outlook desktop or web** → select the email → **Report** → **Report phishing**

This sends the email to Microsoft for analysis and to your organisation's security team if configured.

### 4. Escalate to the Security Team
A phishing email targeting your organisation is a security incident regardless of whether anyone clicked it. Escalate immediately:
- Notify the security team with details of the email — sender address, subject line, what it asked for
- The security team can check whether other users received the same email and block the sender at the tenant level via Microsoft Defender for Office 365

### 5. Check if Anyone Else Received It
Ask colleagues or check with the security team whether the phishing email was sent to multiple users. A targeted campaign across the organisation is a higher severity incident.

---

## Escalate If
- Any user clicked a link or entered credentials — escalate to the security team immediately, this is a potential account compromise
- Multiple users received the same email — escalate, this is an active phishing campaign targeting the organisation
- The sender domain is spoofing the organisation's own domain — escalate urgently, this may require DNS record changes (SPF, DKIM, DMARC)

---

## Notes
- IT will never send emails asking users to click a link and enter their password urgently — this is a fundamental security awareness point worth communicating to the user
- The display name of an email is not the sender address — always check the actual address
- Do not attempt to block the sender yourself at 1st line — this is handled by the security team via the email security platform
- If a user did click a link, treat it as a security incident immediately: reset password, revoke sessions, reset MFA, escalate
