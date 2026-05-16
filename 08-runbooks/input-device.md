# Runbook — Keyboard and Mouse Not Working

## Scenario
A user calls saying their keyboard and mouse have completely stopped working on their laptop. They cannot type or click anything. They are calling from their personal phone.

---

## Steps

### 1. Verify Identity
The user is calling from their personal phone and cannot access their device. Verify identity using knowledge-based questions:
- Employee ID number
- Date of birth
- Manager's name

### 2. Restart via Power Button
The simplest and most effective first step. A driver crash or software hang causes the majority of input device failures and is resolved by a clean restart.

Ask the user to:
1. Hold the power button down until the device shuts off completely
2. Wait 10 seconds
3. Press the power button to restart

Confirm with the user that the keyboard and mouse are working after restart before proceeding.

### 3. If Input Devices Work After Restart
- Ask the user to test both keyboard and mouse thoroughly
- Open Device Manager (search in Start) and check for any yellow warning icons on input device drivers
- Document the incident and monitor — if it happens again it may be a driver issue worth escalating

### 4. If Input Devices Still Not Working After Restart

**Test with external USB devices:**
Ask the user to plug in an external USB keyboard and mouse if available.

- **External devices work** — the issue is with the built-in keyboard/trackpad. Likely a driver issue.
- **External devices also do not work** — the issue is hardware or a deeper software fault. Likely a hardware failure.

**Driver issue (built-in devices not working, USB works):**
Escalate to 2nd line for driver reinstallation or rollback via Device Manager.

**Hardware fault (nothing works, including USB):**
Escalate for physical inspection and potential device replacement.

### 5. Remote Actions via Intune
Remote restart via Intune is an option but requires the device to be connected and responsive enough to receive the command. If the device is completely frozen, the power button is more reliable.

[intune.microsoft.com](https://intune.microsoft.com) → **Devices** → **All devices** → select the device → **Restart**

---

## Escalate If
- Input devices are still not working after restart and external USB devices also fail — escalate for hardware inspection
- Built-in keyboard/trackpad not working but USB works — escalate to 2nd line for driver reinstall
- The device will not power on at all — escalate for hardware repair or replacement

---

## Notes
- A restart resolves the majority of input device issues — always try this first before any remote actions or driver investigation
- Ask about what happened before the issue — a spill, drop, or recent Windows update narrows the cause quickly
- If the device was recently updated, a driver rollback may be needed — check the update history in Windows Update
