# Setup

This guide covers preparing devices for Intune enrolment — creating VMs in VirtualBox and installing Windows 11 Pro on both virtual and physical machines. The goal is a clean Windows 11 Pro installation signed into a local administrator account, ready for Entra ID join and MDM enrolment.

---

## Virtual Machine Setup (VirtualBox)

### Create the VM

1. Open VirtualBox → click **New**
2. Set the following:

| Setting | Value |
|---|---|
| **Name** | WIN-VM-01 (or WIN-VM-02) |
| **ISO Image** | Select your Windows 11 Pro ISO |
| **Skip Unattended Installation** | ✅ Tick this |
| **Base Memory** | 4096 MB (4 GB) |
| **Processors** | 4 |
| **Disk Size** | 80 GB |

> **Skip Unattended Installation must be ticked.** If left unticked, VirtualBox will automatically create a standard user account with no admin rights, which will block Company Portal from enrolling the device later.

3. Leave the network adapter enabled — Windows 11 Pro setup will offer a domain join option without needing to disconnect it
4. Click **Finish**

### Install Windows 11 Pro

1. Start the VM — it will boot from the ISO
2. Select language, time, and keyboard → **Next** → **Install now**
3. When asked for a product key click **I don't have a product key**
4. Select **Windows 11 Pro** → **Next**
5. Accept the licence terms → **Next**
6. Select **Custom: Install Windows only (advanced)**
7. Select the unallocated disk → **Next** — Windows will begin installing and restart automatically

### Set Up a Local Administrator Account

After the first restart, Windows will run through OOBE (Out of Box Experience):

1. Select region and keyboard layout
2. On the **Sign in with Microsoft** screen click **Sign-in options**
3. Select **Join a domain** (some builds label this **Domain join instead**)
4. Enter a local username — use something generic like `User` or `Admin`, not a name that resembles a work account
5. Set a password and security questions
6. Complete the remaining OOBE screens (privacy settings etc.)

> The first account created during Windows setup is always a local Administrator. This is important — Company Portal requires local admin rights to enrol the device.

---

## Physical Device Setup

If setting up a laptop or PC from a fresh Windows installation via the Microsoft Media Creation Tool:

### Windows 11 Pro — Domain Join

1. On the **Sign in with Microsoft** screen click **Sign-in options**
2. Select **Join a domain**
3. Enter a local username and password
4. Complete OOBE

### Windows 11 Home — Fake Microsoft Account

If the device shipped with Windows 11 Home and you are not reinstalling:

1. On the sign-in screen enter `no@thankyou.com` as the email
2. Enter anything as the password
3. The authentication will fail and drop you into local account setup

> Reinstalling as Windows 11 Pro is recommended for this lab — the **Join a domain** option is cleaner and more reliable. Windows 11 Pro ISOs are available via the [Microsoft Media Creation Tool](https://www.microsoft.com/en-gb/software-download/windows11).

---

## Verification Checklist

- [ ] VM or device is running Windows 11 Pro
- [ ] Signed into a **local Administrator** account
- [ ] Network adapter is enabled and internet access confirmed
- [ ] No Microsoft personal account signed in

---

*Next: [Enrolment](./enrolment.md)*