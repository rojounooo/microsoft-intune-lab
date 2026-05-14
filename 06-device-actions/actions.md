# 07 · Device Actions

---

## What I Learnt

### 1. What are device actions?

Device actions are remote management commands sent from Intune to a managed device. They allow an IT engineer to perform common support and security tasks without physical access to the device — useful for remote workers, lost devices, or offboarding scenarios.

Actions are triggered from the device page in Intune: **Devices** → **All devices** → click a device. They appear as buttons across the top of the device overview.

Most actions are asynchronous — Intune queues the command and the device executes it on its next check-in. Triggering a **Sync** first ensures the device picks up the command quickly rather than waiting for the next scheduled check-in.

---

### 2. Common 1st line device actions

| Action | What it does | Re-enrolment required? |
|---|---|---|
| **Sync** | Forces the device to check in with Intune immediately. First step when troubleshooting a policy not applying or a stale compliance status. | No |
| **Restart** | Remotely restarts the device. Useful after policy changes or when a user reports issues and you need a clean boot without asking them to do it. | No |
| **Remote lock** | Locks the device screen immediately and requires a PIN to unlock. Used when a device is reported unattended or missing but not yet confirmed lost. | No |
| **Quick scan** | Triggers a Microsoft Defender quick scan on the device remotely. Scans common malware locations without a full disk scan. | No |
| **Full scan** | Triggers a full Microsoft Defender scan of the entire device. Takes longer but is more thorough. Used when a threat is suspected. | No |
| **Retire** | Removes company data, apps, and policies pushed by Intune, and unenrols the device from management. Personal data and locally installed apps are left intact. Used when an employee leaves the organisation. | Yes — if the device needs to be managed again |
| **Wipe** | Factory resets the device entirely, removing all data, apps, and settings. Used for lost or stolen devices, or when a device is being decommissioned. | Yes |

> **Note on Wipe vs Retire:** Both remove the device from Intune management but Wipe is destructive — all data is gone. Retire is the safer option for offboarding as it only removes company-managed content. Always confirm with a manager before wiping a device.

---

## Performing Device Actions

All device actions are performed from the same place:

[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → click the target device

---

### Sync

1. Click **Sync** in the action bar
2. Confirm the prompt
3. The device will check in with Intune within a few minutes
4. Refresh the device page — **Last check-in** time will update

**When to use:** Any time a policy change is not reflecting on the device, or the compliance status looks stale.

---

### Restart

1. Click **Restart** in the action bar
2. Confirm the prompt
3. The device will restart on its next Intune check-in

> **Note:** The user will receive a notification before the restart on managed devices. The restart will not interrupt a user mid-task immediately — it queues and executes on check-in.

---

### Remote Lock

1. Click **Remote lock** in the action bar
2. Confirm the prompt
3. The device screen will lock and require a PIN or password to unlock

**When to use:** Device reported left unattended in a public place, or a user reports their device is missing but it has not been confirmed stolen yet.

---

### Quick Scan

1. Click **Quick scan** in the action bar
2. Confirm the prompt
3. Defender will run a scan on the device — results will appear in the device's Defender reports in Intune

---

### Full Scan

1. Click **Full scan** in the action bar
2. Confirm the prompt
3. Defender will run a full disk scan — this may take a significant amount of time depending on disk size

**When to use:** A threat has been detected or suspected, or a quick scan returned inconclusive results.

---

### Retire

> **⚠ Re-enrolment required after this action.**
> The device will be unenroled from Intune. To bring it back under management, re-enrol via Company Portal. If using VMs, taking a snapshot before performing this action avoids the need to re-enrol.

1. Click **Retire** in the action bar
2. Confirm the prompt
3. Intune will remove all company data, policies, and apps from the device on its next check-in
4. The device will disappear from **All devices** in Intune once the action completes

**What is removed:**
- Intune configuration profiles and compliance policies
- Apps deployed as Required by Intune
- Company email and data managed by Intune

**What is kept:**
- Locally installed apps not deployed by Intune
- Personal files and data
- The Windows installation itself

---

### Wipe

> **⚠ Re-enrolment required after this action. All data will be permanently deleted.**
> This action factory resets the device. If using VMs, take a snapshot before performing this action to avoid a full Windows reinstall.

1. Click **Wipe** in the action bar
2. You will be presented with options:
   - **Wipe device and continue to enrol** — resets and re-enrols automatically (requires Autopilot)
   - **Wipe device and do not continue to enrol** — full factory reset, no automatic re-enrolment
3. Confirm the prompt
4. The device will factory reset on its next check-in

**When to use:** Lost or stolen device confirmed, or device being decommissioned and wiped for reuse.

---

## Lab Checklist

> **Tip:** Take a VM snapshot before performing Retire and Wipe to avoid re-enrolling from scratch each time.

- [ ] **Sync** — triggered and Last check-in time updated
- [ ] **Restart** — triggered and device restarted
- [ ] **Remote lock** — triggered and device locked
- [ ] **Quick scan** — triggered and scan completed
- [ ] **Full scan** — triggered and scan completed
- [ ] **Retire** — triggered, device removed from Intune, re-enrolled afterwards
- [ ] **Wipe** — triggered, device factory reset, re-enrolled afterwards

---

## Useful Links

| Resource | URL |
|---|---|
| Intune Admin Centre | [intune.microsoft.com](https://intune.microsoft.com) |
| Device actions documentation | [learn.microsoft.com/en-us/mem/intune/remote-actions/device-management](https://learn.microsoft.com/en-us/mem/intune/remote-actions/device-management) |

---

*Previous: [06 · Conditional Access](../06-conditional-access/) · Next: [08 · Autopilot](../08-autopilot/)*