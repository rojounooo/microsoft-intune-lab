# Runbook — Password Change Failing

## Scenario
A user is being prompted to change their password but every attempt fails with a message saying the password does not meet requirements.

---

## Steps

### 1. Verify Identity
Confirm the caller is who they say they are before discussing or resetting their account.

### 2. Check for Account Lockout
Multiple failed password attempts may have triggered a lockout. Check before attempting anything else:

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Sign-in logs** — look for repeated failed attempts

If locked out, unlock the account before proceeding.

### 3. Explain the Password Requirements Clearly
Tell the user exactly what the policy requires — do not just say "it needs to be complex":
- Minimum 8 characters
- Mix of letters and numbers (alphanumeric)
- Cannot reuse the last 5 passwords
- No simple patterns (e.g. `Password1`, `12345678`)

Users often fail because they are trying a slight variation of an old password, which gets blocked by the history policy.

### 4. Check the Password Policy in Intune
[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **Configuration** → open the password configuration profile → confirm the current settings

Cross reference with what the user is attempting to set to identify what is failing.

### 5. Check Group Membership
Confirm the user is assigned to the correct group that the password policy is targeting:

[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Groups**

### 6. Reset the Password and Walk Them Through It
1. [admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the user → **Reset password**
2. Note the temporary password and communicate it securely
3. Stay on the call while the user signs in with the temp password and is prompted to set a new one
4. Guide them through choosing a compliant password
5. Confirm the new password is accepted before ending the call

---

## Escalate If
- The account is locked and you do not have authority to unlock it — escalate to 2nd line
- The password policy appears misconfigured — escalate to 2nd line to review the configuration profile
- The user is unable to set a compliant password after multiple assisted attempts — escalate

---

## Notes
- Always walk the user through setting the new password on the call — do not send a reset link and end the call, the same problem will occur when they try to set the new one
- The most common failure reason is the password history policy — users try their old password with a minor change
- If the compliance policy is flagging password complexity but no configuration profile is enforcing it, the check will keep failing regardless of the password — the configuration profile must be in place for the compliance check to pass
