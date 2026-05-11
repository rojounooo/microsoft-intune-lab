# Enrolment

This guide covers enrolling a prepared Windows 11 Pro device into Microsoft Intune. Complete [Setup](./setup.md) before proceeding.

---

## What I Learnt

### 1. Entra ID Join vs MDM Enrolment — two separate steps

With **Entra ID P1** (not included in the free Intune trial), joining a device to Entra ID automatically triggers Intune enrolment in a single step. Without it, they are two separate steps:

1. **Entra ID Join** — the device gets an identity in your directory. Entra ID knows it exists and who it belongs to.
2. **MDM Enrolment** — the device registers with Intune so policies can be pushed to it. Done manually via the Company Portal app.

Both steps are required. A device that is Entra joined but not MDM enrolled will appear in Entra ID but not in Intune, and no policies will apply to it.

### 2. Company-owned vs BYOD enrolment

During enrolment you will see two options under Settings → Accounts → Access work or school:

| Option | What it does | Use case |
|---|---|---|
| **Join this device to Microsoft Entra ID** | Full Entra join — employer has full MDM control over the whole device | Company-owned device |
| **Enrol only in device management** | MDM enrolment without full Entra join — employer manages apps only | BYOD (personal device) |

This lab uses full Entra join to simulate company-owned device management.

### 3. Company Portal

The Company Portal app is the Microsoft-provided MDM enrolment agent for Windows. It handles the MDM enrolment step and gives end users a self-service portal to view enrolled devices, install approved apps, and check compliance status.

Without Entra P1, Company Portal must be installed and signed into manually after the Entra join — it will not trigger automatically.

### 4. Local admin rights are required for enrolment

Company Portal requires the signed-in Windows account to have local administrator rights. If the local account is a standard user, Company Portal will throw a privileges error and enrolment will fail. This is why the local account must be set up as an Administrator during Windows setup.

---

## Prerequisites

Before enrolling, confirm the following:

- [ ] Device has completed [Setup](./setup.md) and is signed into a local Administrator account
- [ ] MDM authority set to `Microsoft Intune` in the Intune admin centre
- [ ] Entra ID device join permitted for all users
- [ ] The user account being used has an **Intune licence** assigned in M365 Admin Centre
- [ ] Temporary password for the user account noted

> **Licence error in Company Portal:** If Company Portal says a licence is required, go to [admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select the user → **Licenses and apps** and confirm Microsoft Intune is ticked. Wait 5 minutes after assigning before trying again.

---

## Step 1 — Join the Device to Entra ID

1. **Settings** → **Accounts** → **Access work or school** → **Connect**
2. Click **Join this device to Microsoft Entra ID** — do not type the email straight into the top box, this option is further down and easy to miss
3. Sign in with the lab user account for this device:

| Device | Account |
|---|---|
| WIN-VM-01 | client01@rojolabs.onmicrosoft.com |
| WIN-VM-02 | client02@rojolabs.onmicrosoft.com |
| LAPTOP-01 | client01@rojolabs.onmicrosoft.com |

4. Review the confirmation screen — confirm the tenant name is correct → click **Join**
5. When prompted to add an account to the device, click **Skip**
6. Restart the device

> **After restart:** on the login screen select **Other user** and sign in with the Entra lab user account. Do not sign back into the local account — signing in as the Entra user is what completes the join and triggers the initial policy sync.

---

## Step 2 — Enrol into Intune via Company Portal

1. Signed in as the Entra user, open the **Microsoft Store**
2. Search for **Company Portal** → install it
3. Open Company Portal and sign in with the same lab user account used during the Entra join
4. On the home screen you will see **This device hasn't been set up for corporate use yet** — click it
5. Follow the enrolment prompts through to completion
6. The device will appear under **My Devices** in Company Portal once done

> **Privileges error:** If Company Portal says you do not have the right privileges, the local account used during Windows setup was a standard user, not an Administrator. Rebuild the VM following the [Setup](./setup.md) guide and ensure **Skip Unattended Installation** is ticked.

---

## Step 3 — Verify Enrolment in Intune

1. Go to [intune.microsoft.com](https://intune.microsoft.com)
2. **Devices** → **All devices**
3. The enrolled device should appear within a few minutes

> **Device not appearing:** Intune can be slow to register newly enrolled devices. Wait 5 minutes and refresh. If it still does not appear, go to **Settings** → **Accounts** → **Access work or school** → click the work account → **Info** → **Sync** to force an immediate check-in with Intune.

> **Two entries in Access work or school:** After completing both steps, Settings → Accounts → Access work or school will show two entries — one for the Entra join and one for MDM enrolment. This is expected and correct.

---

## Enrolled Devices

| Device | Entra Joined | MDM Enrolled | Intune User |
|---|---|---|---|
| `WIN-VM-01` | [ ] | [ ] | client01 |
| `WIN-VM-02` | [ ] | [ ] | client02 |
| `LAPTOP-01` | [ ] | [ ] | client01 |

---

## Verification Checklist

- [ ] All devices joined to Entra ID
- [ ] Company Portal installed and signed into on all devices
- [ ] All devices visible under Devices → All devices in Intune
- [ ] All devices show correct user assignment in Intune

---

## Useful Links

| Resource | URL |
|---|---|
| Intune Admin Centre | [intune.microsoft.com](https://intune.microsoft.com) |
| Entra Admin Centre | [entra.microsoft.com](https://entra.microsoft.com) |
| M365 Admin Centre | [admin.microsoft.com](https://admin.microsoft.com) |
| Company Portal (Microsoft Store) | [aka.ms/intune-cp](https://aka.ms/intune-cp) |

---

*Previous: [Setup](./setup.md) · Next: [03 · Compliance Policies](../03-compliance-policies/)*