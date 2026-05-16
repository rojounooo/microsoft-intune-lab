# 08 · Autopilot

---

## What I Learnt

### 1. What is Autopilot?

Windows Autopilot is Microsoft's zero-touch device provisioning system. Rather than IT manually setting up each device before handing it to a user, Autopilot allows a new laptop to be shipped directly from a supplier to an employee. The user turns it on, signs in with their work account, and Intune automatically configures everything — policies, apps, and settings — without IT ever physically touching the device.

This is how most large enterprises deploy endpoints at scale. From an IT support perspective, Autopilot shifts the provisioning model from:

```
IT receives device → manually configures it → ships to user
```
to:
```
Supplier ships device directly to user → user signs in → device self-configures
```

Autopilot handles the Out-of-Box Experience (OOBE) — the setup screens a user sees when turning on a new Windows device. An Autopilot deployment profile controls which screens are shown or hidden, what account type the user gets, and how the device joins Entra ID.

In this lab, Autopilot successfully configured the OOBE on a VM — skipping the EULA, privacy settings, and keyboard selection screens, and going straight to the work account sign-in. Auto-enrolment into Intune did not trigger because that requires **Entra ID P1**, which is not included in the free trial. Manual enrolment via Company Portal is required instead.

### 2. How to get a device hardware hash

Autopilot identifies devices by their **hardware hash** — a unique fingerprint generated from the device's hardware components. Before a device can receive an Autopilot profile, its hash must be registered in Intune.

The hash is extracted using the **Get-WindowsAutopilotInfo** PowerShell script, run on the device itself.

1. Open PowerShell as Administrator on the device
2. First, set the execution policy to allow the script to run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned -Force
```

3. Install and run the script:

```powershell
Install-Script -Name Get-WindowsAutopilotInfo -Force
Get-WindowsAutopilotInfo -OutputFile C:\hwid.csv
```

4. Type `Y` when prompted to install from PSGallery
5. The script will generate `hwid.csv` at `C:\` containing the device's hardware hash

> **Gotcha — Execution Policy:** Running `Get-WindowsAutopilotInfo` without first setting the execution policy will throw an `UnauthorizedAccess` error. Always run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned -Force` first.

> **Note — VMs:** Hardware hashes extracted from VirtualBox VMs will show `To be filled by O.E.M` for the manufacturer and serial number fields, and the hash itself may end in a long string of `A`s. This is expected — VirtualBox does not populate BIOS fields the way physical hardware does. The hash will still register successfully in Intune.

### 3. How to import the hash into Intune

1. Transfer `hwid.csv` from the device to the machine you use to access Intune — install **VirtualBox Guest Additions** on the VM first to enable drag and drop and shared clipboard (**Devices** → **Insert Guest Additions CD image** inside the VM)
2. In Intune, navigate to:
**Devices** → **Device Onboarding** → **Enrollment** → **Windows** → **Windows Autopilot** → **Devices** → **Import**
3. Select the `hwid.csv` file → **Import**
4. The device will appear in the Autopilot devices list within a few minutes

### 4. How to create an Autopilot deployment profile

An Autopilot deployment profile controls the OOBE experience for registered devices.

1. **Devices** → **Device Onboarding** → **Enrollment** → **Windows** → **Windows Autopilot** → **Deployment Profiles** → **Create profile** → **Windows PC**
2. Give the profile a name and click **Next**
3. Configure the OOBE settings:

| Setting | Value | Why |
|---|---|---|
| **Deployment mode** | User-Driven | User signs in with their work account during setup |
| **Join to Microsoft Entra ID as** | Microsoft Entra joined | Cloud only, no on-prem AD |
| **Microsoft Software License Terms** | Hide | Skips the EULA screen |
| **Privacy settings** | Hide | Skips privacy screens |
| **Hide change account options** | Hide | Prevents switching accounts during setup |
| **User account type** | Standard | End users should not be local admins |
| **Allow pre-provisioned deployment** | No | Requires specialist hardware |
| **Automatically configure keyboard** | Yes | Skips keyboard selection screen |
| **Apply device name template** | Yes | e.g. `LAB-%RAND:4%` generates names like `LAB-A3F2` |

4. Click **Next** → assign to the Autopilot Devices group (see below) → **Create**

### 5. Autopilot devices need their own Entra ID group

Autopilot deployment profiles are assigned to groups, the same as compliance policies and configuration profiles. However, Autopilot profiles should be assigned to a group containing **device objects**, not user accounts.

When a device's hardware hash is imported into Intune, a corresponding device object is created in Entra ID. A dedicated security group must be created and the imported device added to it before the profile can be assigned.

1. [entra.microsoft.com](https://entra.microsoft.com) → **Groups** → **All groups** → **New group**

| Setting | Value |
|---|---|
| **Group type** | Security |
| **Group name** | Autopilot Devices |
| **Membership type** | Assigned |

2. Under **Members**, add the imported Autopilot device object
3. Assign the deployment profile to this group

> **Note:** Dynamic device groups (e.g. automatically adding all Autopilot-registered devices) require **Entra ID P1**. With the free trial, devices must be added to the group manually.

### 6. Account Switching: 
When a device is set up manually, a local account is created first and the work account is added on top. This means the user can switch between them at the login screen. In an enterprise environment this is a security risk since the local account isn't managed by Intune and could be used to bypass policies. Autopilot eliminates this by removing the local account creation step entirely; the work account is the only account on the device from first boot.

### 7. Standard User vs Admin Account:
With manual setup, the first account created during Windows installation is always a local Administrator. Autopilot lets you enforce Standard user as the account type in the deployment profile, meaning end users never have local admin rights from the start. This is best practice in enterprise environments; users shouldn't be able to install software, change system settings, or bypass security controls.

---

## Triggering an Autopilot Reset

To test the Autopilot profile on a VM:

1. Inside the VM: **Settings** → **System** → **Recovery** → **Reset this PC** → **Remove everything** → **Local reinstall** → **Reset**
2. The VM will wipe and reboot into OOBE
3. The Autopilot profile will be applied — configured screens will be skipped and the device will go straight to the work account sign-in

> **Gotcha — VM reset time:** Resetting a VM can take up to 30 minutes depending on the host machine's hardware. This is significantly longer than a physical device reset. Plan accordingly and do not interrupt the process.

---

## Limitations in This Lab

| Limitation | Reason |
|---|---|
| Auto-enrolment into Intune did not trigger after Autopilot | Requires Entra ID P1, not included in the free trial |
| Dynamic Autopilot device groups not available | Requires Entra ID P1 |

---

## Verification Checklist

- [ ] Hardware hash extracted from device using Get-WindowsAutopilotInfo
- [ ] Hash imported into Intune — device visible in Autopilot Devices list
- [ ] Autopilot Devices group created in Entra ID
- [ ] Deployment profile created and assigned to Autopilot Devices group
- [ ] VM reset triggered and Autopilot OOBE confirmed — EULA, privacy, and keyboard screens skipped

---

## Useful Links

| Resource | URL |
|---|---|
| Intune Admin Centre | [intune.microsoft.com](https://intune.microsoft.com) |
| Get-WindowsAutopilotInfo | [powershellgallery.com/packages/Get-WindowsAutopilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) |
| Autopilot documentation | [learn.microsoft.com/en-us/autopilot](https://learn.microsoft.com/en-us/autopilot) |

---

*Previous: [06 · Device Actions](../06-device-actions/) · Next: [08 · Runbooks](../08-runbooks/)*