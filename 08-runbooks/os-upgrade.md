# Runbook — Windows Upgrade Request

## Scenario
A user's laptop is running Windows 10 and they are receiving notifications about a Windows 11 upgrade. They want to know if they should upgrade and how to do it.

---

## Steps

### 1. Determine if it is a Company or Personal Device

**Personal device:**
Walk the user through the upgrade directly. Check hardware compatibility first (TPM 2.0, Secure Boot, 4GB RAM minimum, 64GB storage) then:
**Settings** → **Windows Update** → **Check for updates** → follow the prompts if Windows 11 is available.

**Company device:**
Do not advise the user to upgrade themselves. Continue with the steps below.

### 2. Check the Organisation's Windows Update Policy
On a managed company device, OS upgrades are controlled centrally via Intune **Windows Update rings** — a configuration profile that determines which updates devices receive and when.

Check whether Windows 11 is the current approved OS version for managed devices in your organisation. If Windows 10 is still the standard:
- The device is likely compliant as is
- Advise the user not to upgrade
- Reassure them the notification is from Windows, not an Intune requirement

### 3. Advise the User
If Windows 10 is still the approved standard:
- Inform the user that upgrades are managed centrally by IT
- Advise them to dismiss the notification
- Confirm their device is compliant and working correctly

If Windows 11 is being rolled out:
- Confirm whether the user's device is in the current upgrade wave
- If not yet included, advise them it will be pushed automatically when their device is next in the rollout schedule

### 4. Do Not Allow Self-Initiated Upgrades on Company Devices
Standard users should not be able to initiate a major OS upgrade on a managed device. If the user has admin rights and is asking permission — advise them not to proceed and escalate to confirm whether their device should be upgraded.

---

## Escalate If
- The user wants to upgrade and their device is not yet in the rollout schedule — escalate to 2nd line to confirm the plan
- The user has already upgraded without authorisation and is experiencing issues — escalate to 2nd line
- The organisation has not yet tested Windows 11 compatibility with line-of-business apps — escalate any upgrade requests

---

## Notes
- In a properly managed Intune environment, OS upgrades are handled via Windows Update rings — rolled out in waves, with a small pilot group tested first. Self-initiated upgrades bypass this process entirely
- Compatibility issues with line-of-business apps are the most common reason organisations delay Windows 11 adoption — never assume an upgrade is safe without IT sign-off on company devices
- For personal devices, TPM 2.0 is the most common hardware compatibility blocker — if the device does not meet requirements, advise the user to check with their PC manufacturer
