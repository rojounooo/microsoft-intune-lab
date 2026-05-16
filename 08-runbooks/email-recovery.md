# Runbook — Deleted Email Recovery

## Scenario
A user has accidentally deleted an important email and needs it recovered. They deleted it approximately 3 days ago.

---

## Steps

### 1. Check the Deleted Items Folder
Ask the user to check their Deleted Items folder in Outlook first. Most users do not realise deleted emails go here rather than being permanently deleted immediately.

If the email is there, the issue is resolved — no admin action required.

### 2. Check Recoverable Items
If the user has emptied their Deleted Items folder, emails move to a hidden **Recoverable Items** folder. Items remain here for **14 days** by default before permanent deletion.

The user can access this themselves:

**Outlook desktop:**
1. Click the **Deleted Items** folder
2. At the top of the folder click **Recover items recently removed from this folder**
3. Search for the email and click **Restore**

**Outlook on the web:**
1. Go to the **Deleted Items** folder
2. Click **Recover items deleted from this folder** at the top

Since the email was deleted 3 days ago it should still be in Recoverable Items.

### 3. If the User Cannot Find it in Recoverable Items
If the email is not visible to the user, an admin can search and restore it via the **Microsoft Purview compliance portal**:

[compliance.microsoft.com](https://compliance.microsoft.com) → **Content search** → create a new search targeting the user's mailbox

This level of access is typically above 1st line. Raise a request with 2nd line or whoever manages the compliance portal in your organisation.

---

## Escalate If
- The email is not in Deleted Items or Recoverable Items and admin search is required — escalate to 2nd line or IT admin with compliance portal access
- The email was deleted more than 14 days ago — the default retention period may have passed. Escalate to check if extended retention policies are in place
- The user needs emails recovered in bulk — escalate to 2nd line

---

## Notes
- 3 days ago is well within the 14-day Recoverable Items retention period — always check there before escalating
- Walk the user through checking Recoverable Items themselves before raising an admin request — it is quicker and gives the user a useful skill
- Retention periods may vary if the organisation has custom retention policies configured in Microsoft Purview — check with 2nd line if the standard 14 days does not apply
