# 01 · Tenant Setup

---

## What I Learnt

### 1. What is Intune and what is Entra ID?

**Entra ID** is Microsoft's cloud-based identity service. It handles users, groups, and device identities — the cloud equivalent of on-premises Active Directory.

**Microsoft Intune** is Microsoft's cloud MDM (Mobile Device Management) platform. It sits on top of Entra ID and uses its identities to manage devices — the cloud equivalent of Group Policy. 

### 2. What is a licence and how do you assign one?

In Microsoft's ecosystem, features are tied to licences rather than being on or off by default. A user account without a licence just exists but has no access to any services. Without a licence, a user cannot access any Microsoft services. Intune licences were assigned to the lab users via the Microsoft 365 Admin Centre. 

The licences used in this lab are:

| Licence | Perks |
|---|---|
| **Entra ID Free** | Basic directory — logins, device join, group membership. Every account gets this by default. |
| **Microsoft Intune Plan 1** | Allows a user's device to be managed by Intune. Without this, Company Portal will throw a licence error and the device cannot enrol. |

> **Note:** **Entra ID P1** is not included in the free Intune trial. This means that automatic MDM enrolment is not available. Devices must be enrolled manually via the Company Portal app after joining Entra ID. 

The Intune free trial includes 25 Intune Plan 1 licences. This means up to 25 user accounts can have devices managed by Intune, though you can create far more than 25 accounts in the tenant — unlicenced accounts simply cannot enrol devices.

Licences are assigned per user in the **Microsoft 365 Admin Centre** (not Intune or Entra — those portals link you back to M365 Admin Centre for licence management):

1. [admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select a user
2. **Licenses and apps** tab → tick **Microsoft Intune** → **Save changes**

> **Gotcha:** There can be a sync delay of several minutes after assigning a licence before the user can sign into Company Portal. If you get a licence error immediately after assigning, wait several minutes and try again.

### 3. Setting up an Intune tenant

#### Signing up via the Intune free trial

The free trial is available at [aka.ms/intunetrial](https://aka.ms/intunetrial). A credit card is required at signup however recurring billing is turned off by default. The trial runs for 30 days and includes Intune Plan 1 with 25 licences.

> **Note:** Confirm that recurring billing is turned off in [admin.microsoft.com](https://admin.microsoft.com) → **Billing** → **Your products**.

> **Alternative:** Many universities provide free Visual Studio Professional or Enterprise subscriptions, which grant access to the Microsoft 365 Developer Programme — a free, renewable E5 tenant that includes Intune. Check your university's software portal before signing up for the trial.

#### Setting up 2FA

Securing the admin account with MFA is important — this account has full control over all managed devices in the tenant.

1. Go to [aka.ms/mfasetup](https://aka.ms/mfasetup) and sign in with the admin account
2. Select **Add sign-in method** → **Authenticator app**
3. Scan the QR code with your authenticator app of choice

[Aegis](https://getaegis.app/) (Android, open source) works well for this — setup is as simple as scanning the QR code. Microsoft Authenticator also works if you prefer to stay in the Microsoft ecosystem.

#### Creating user accounts

Dedicated user accounts should be created for device enrolment rather than using the admin account. In a real environment, end users have their own accounts and IT admins have separate privileged accounts.

1. [intune.microsoft.com](https://intune.microsoft.com) → **Users** → **All users** → **New user**
2. Create the following accounts (adjust the tenant domain to match yours):

| Display Name | Username | Role |
|---|---|---|
| Client 01 | client01@\<yourtenant\>.onmicrosoft.com | Member |
| Client 02 | client02@\<yourtenant\>.onmicrosoft.com | Member |

3. Note the temporary passwords — you will need these during device enrolment

> **User type — Member vs Guest:** When creating accounts you will see the user type shown as **Member** in Entra ID. This is the directory role (a regular internal account, as opposed to a Guest which is an externally invited user). This is unrelated to whether the account has local administrator rights on a device.

#### Attaching licences to users

After creating the accounts, assign Intune licences via the M365 Admin Centre:

1. [admin.microsoft.com](https://admin.microsoft.com) → **Users** → **Active users** → select **client01**
2. **Licenses and apps** tab → tick **Microsoft Intune** → **Save changes**
3. Repeat for **client02**

> The Intune free trial includes **25 licences**. You can create as many user accounts as you like in the tenant, but only 25 of them can have Intune assigned and therefore have devices managed by Intune.

---

## Tenant Configuration

### 1. Verify MDM Authority

1. [intune.microsoft.com](https://intune.microsoft.com) → **Tenant administration** → **Tenant status**
2. Confirm **MDM authority** is set to `Microsoft Intune`

### 2. Automatic Enrolment

> **Note:** Automatic MDM enrolment (where a device auto-enrolls into Intune the moment it joins Entra ID) requires **Entra ID P1**, which is not included in the free Intune trial. Without it, devices must be enrolled manually via the Company Portal app after joining Entra ID. See [02 · Device Enrolment](../02-device-enrolment/) for the manual enrolment process.

### 3. Configure Entra ID Device Join

1. [entra.microsoft.com](https://entra.microsoft.com) → **Devices** → **Device settings**
2. Set **Users may join devices to Entra ID** to `All`
3. Set **Maximum number of devices per user** to `20`
4. Click **Save**

---

## Verification Checklist

- [x] Signed in to [intune.microsoft.com](https://intune.microsoft.com) successfully
- [x] MDM authority confirmed as `Microsoft Intune`
- [x] Recurring billing cancelled (trial users)
- [x] Admin account secured with MFA
- [x] Entra ID device join permitted for all users
- [x] client01 and client02 accounts created
- [x] Intune licence assigned to client01 and client02

---

## Useful Links

| Resource | URL |
|---|---|
| Intune Free Trial | [aka.ms/intunetrial](https://aka.ms/intunetrial) |
| Intune Admin Centre | [intune.microsoft.com](https://intune.microsoft.com) |
| Entra Admin Centre | [entra.microsoft.com](https://entra.microsoft.com) |
| M365 Admin Centre | [admin.microsoft.com](https://admin.microsoft.com) |
| MFA Setup | [aka.ms/mfasetup](https://aka.ms/mfasetup) |
| Aegis Authenticator | [getaegis.app](https://getaegis.app/) |
| M365 Developer Programme | [developer.microsoft.com/microsoft-365/dev-program](https://developer.microsoft.com/microsoft-365/dev-program) |

---

*Next: [02 · Device Enrolment](../02-device-enrolment/)*