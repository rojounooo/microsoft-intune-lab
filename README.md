# Microsoft Intune
> **Self-directed** · Microsoft Intune · Microsoft 365 Developer Tenant

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

## Why
To build practical Mobile Device Management skills using Microsoft Intune. Covering device enrollment, compliance policies, configuration profiles, app deployment, and Conditional Access to demonstrate 1st and 2nd line endpoint management experience.

---

## Notes and Gotchas

Throughout each section you will find `> **Note:**` and `> **Gotcha:**` callouts. These are not copied from documentation — they are things I ran into during the lab and documented as I went. They reflect real troubleshooting experience rather than a clean walkthrough.

---

## Requirements

| | Minimum | Recommended |
|---|---|---|
| **OS** | Windows 10 | Windows 10/11 |
| **RAM** | 8 GB | 16 GB |
| **Storage** | 60 GB free | 100 GB+ free |
| **CPU** | Dual-core, 64-bit | Quad-core, 64-bit |
| **Virtualisation** | VirtualBox | VirtualBox |
| **Internet** | Required — Intune is cloud-only | Stable broadband |
| **Account** | Microsoft 365 Developer Tenant (free) | — |

> Sign up for a free M365 E5 developer tenant (includes Intune) at [developer.microsoft.com/microsoft-365/dev-program](https://developer.microsoft.com/microsoft-365/dev-program). Tenants are free and renewable every 90 days.

---

## Lab Environment

The lab uses a mix of virtual machines and a physical device, all enrolled into a shared Microsoft Intune tenant.

| Device | Role | OS | RAM | Disk | Type |
|---|---|---|---|---|---|
| `WIN-VM-01` | Managed Endpoint | Windows 11 Pro | 4 GB | 80 GB | VirtualBox VM |
| `WIN-VM-02` | Non-compliant Test Device | Windows 11 Pro | 4 GB | 80 GB | VirtualBox VM |
| `LAPTOP-01` | Physical Test Device | Windows 11 Pro | 16GB | 512GB | Physical machine |

**Tooling**

| Tool | Version / Source |
|---|---|
| VirtualBox | 7.x |
| Windows 11 Pro | ISO — [Microsoft Media Creation Tool](https://www.microsoft.com/en-gb/software-download/windows11) |
| Microsoft Intune | Included with M365 E5 developer tenant |
| Win32 Content Prep Tool | [github.com/microsoft/Microsoft-Win32-Content-Prep-Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool) |

> Verify ISO integrity against Microsoft's published SHA-256 checksums before use.

---

## Automation

Where feasible, tasks are automated via PowerShell scripts.

---

## Repository Structure

Each topic area has its own directory for notes, exported policy configs, runbooks, and screenshots.

```
.
├── assets/
├── 01-tenant-setup/
├── 02-device-enrollment/
├── 03-compliance-policies/
├── 04-configuration-profiles/
├── 05-app-deployment/
├── 06-device-actions/
├── 07-autopilot/
├── 08-powershell/
├── 09-runbooks/
├── LICENSE
└── README.md
```

---

## Progress

- [x] 01 · Tenant Setup
- [x] 02 · Device Enrollment
- [x] 03 · Compliance Policies
- [x] 04 · Configuration Profiles
- [x] 05 · App Deployment (Win32)
- [ ] 06 · Device Actions (Wipe, Retire, Sync)
- [ ] 07 · Autopilot
- [ ] 08 · PowerShell
- [ ] 09 · Runbooks

---

## Licence

This repository is licensed under the [MIT License](./LICENSE). You are free to use, adapt, and share the scripts and notes within it.
