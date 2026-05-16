# Runbook — New Starter Cannot Sign In

## Scenario
A new employee has received their company laptop and cannot sign in. They do not know their username or password.

---

## Steps

### 1. Verify Identity
Confirm the caller is who they say they are before sharing any account details. Use at least two of the following:
- Employee ID number
- Date of birth
- Manager's name

Cross-reference against the onboarding list provided by HR. New starters are expected and should be listed.

### 2. Confirm Username
Check the onboarding documentation or welcome email sent by HR. Read the username to the user over the phone or resend the welcome email to their personal address if they have not received it.

> Do not send usernames to unverified personal email addresses.

### 3. Reset Password
1. [admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the user
2. **Reset password** → note the temporary password
3. Communicate the temporary password securely over the phone
4. The user will be prompted to change it on first sign in

### 4. Confirm Sign In
Stay on the call while the user signs in and completes the password change. Confirm Windows Hello is set up if prompted.

### 5. Check Company Portal
- Confirm Company Portal is installed on the device
- If not, walk the user through installing it from the Microsoft Store
- Confirm the device is enrolled and shows in Intune

### 6. Check Compliance
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → confirm the device shows as **Compliant**

### 7. Confirm Access
Ask the user to confirm they can open Outlook, Teams, and any other tools they need for their role.

### 8. Log the Ticket
Document the actions taken, timestamps, and close the ticket.

---

## Escalate If
- The account does not exist in Entra ID — contact HR to confirm the user was set up
- The device is not appearing in Intune — escalate to 2nd line
- The user needs access to shared mailboxes or role-specific systems — confirm with their manager and raise a separate request

---

## Notes
- Check whether the user needs access to any shared mailboxes for their role and raise a request if so
- Check Entra ID group membership — confirm they are in the correct department and role groups
- Assign their manager in Entra ID if not already set
- For BYOD employees, walk them through adding a work account via Settings → Accounts → Access work or school, then installing and enrolling via Company Portal
