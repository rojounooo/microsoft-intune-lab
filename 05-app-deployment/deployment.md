# 05 · App Deployment (Win32)

---

## What I Learnt

### 1. What is the Win32 Content Prep Tool?

Intune cannot deploy standard `.msi` or `.exe` installers directly. Instead, they must be packaged into the `.intunewin` format first — a compressed, encrypted wrapper that Intune can distribute and track.

The **Microsoft Win32 Content Prep Tool** (`IntuneWinAppUtil.exe`) is a command-line utility that handles this conversion. It takes an installer file as input and outputs a single `.intunewin` file ready for upload to Intune.

The tool is free and available on GitHub:
[github.com/microsoft/Microsoft-Win32-Content-Prep-Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool)

### 2. How to use the prep tool

#### What you need

- The installer file - in this lab, `GoogleChromeStandaloneEnterprise64.msi` downloaded from [google.com/chrome/enterprise](https://chromeenterprise.google/browser/download/)
- `IntuneWinAppUtil.exe` downloaded from the GitHub link above
- A source folder containing the installer
- An output folder for the `.intunewin` file

#### Running the tool

Place `IntuneWinAppUtil.exe` and the installer in the same folder, then open Command Prompt in that folder and run:

```cmd
IntuneWinAppUtil.exe -c "C:\path\to\source" -s "GoogleChromeStandaloneEnterprise64.msi" -o "C:\path\to\output"
```

| Flag | What it does |
|---|---|
| `-c` | Source folder containing the installer |
| `-s` | The setup file (the installer) |
| `-o` | Output folder where the `.intunewin` file will be saved |

The tool will generate `GoogleChromeStandaloneEnterprise64.intunewin` in the output folder. This is the file uploaded to Intune.

> **Note:** The `.intunewin` file is encrypted — you cannot open or inspect it after it is created. If you need to make changes to the installer, rerun the prep tool to generate a new package.

Alternatively, run the .exe file and it will guide you through the process. The wizard will ask you the same questions as the command line arguments.

### 3. Pushing required apps to devices

In Intune, apps can be assigned to groups in two ways:

| Assignment type | What it does |
|---|---|
| **Required** | App is automatically installed on the device without user interaction |
| **Available** | App appears in Company Portal for the user to install manually |

Setting an app as **Required** for the Intune Lab Devices group means Intune will push it to every device in that group automatically. The user does not need to do anything — the app installs silently in the background and appears in Company Portal once complete.

---

## Deploying a Win32 App

### Step 1 — Package the installer

1. Download `IntuneWinAppUtil.exe` from [github.com/microsoft/Microsoft-Win32-Content-Prep-Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool)
2. Download the Chrome enterprise MSI from [chromeenterprise.google/browser/download](https://chromeenterprise.google/browser/download/) — select **64-bit MSI**
3. Create two folders — `source` and `output`
4. Place the MSI in the `source` folder
5. Open Command Prompt and run:

```cmd
IntuneWinAppUtil.exe -c "C:\source" -s "GoogleChromeStandaloneEnterprise64.msi" -o "C:\output"
```

6. The `.intunewin` file will appear in the output folder

### Step 2 — Add the app to Intune

1. [intune.microsoft.com](https://intune.microsoft.com) → **Apps** → **All apps** → **Add**
2. App type: **Windows app (Win32)** → **Select**
3. Click **Select app package file** → upload the `.intunewin` file → **OK**
4. Fill in the app information:

| Field | Value |
|---|---|
| **Name** | Google Chrome |
| **Publisher** | Google |
| **Version** | (from the MSI filename or Google's site) |

5. Click **Next**

### Step 3 — Configure install and uninstall commands

Intune needs to know how to install and uninstall the app silently.

| Field | Value |
|---|---|
| **Install command** | `msiexec /i "GoogleChromeStandaloneEnterprise64.msi" /quiet` |
| **Uninstall command** | `msiexec /x {ProductCode} /quiet` |
| **Install behaviour** | System |

> The product code for the uninstall command can be found in the registry at `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall` after Chrome is installed, or from Google's documentation.

### Step 4 — Detection rules

Detection rules tell Intune how to check whether the app is already installed, to avoid reinstalling it unnecessarily.

1. Rule format: **MSI**
2. Intune will auto-populate the MSI product code from the `.intunewin` package — leave it as is

### Step 5 — Assignments

1. Under **Required** click **Add group** → select **Intune Lab Devices** → **Select**
2. Click **Next** → **Review + create** → **Create**

Intune will begin pushing Chrome to all devices in the group. The app will install silently and appear in Company Portal once complete.

---

## Verification Checklist

- [ ] `.intunewin` package created using the Win32 Content Prep Tool
- [ ] App uploaded to Intune with correct install and uninstall commands
- [ ] App assigned as Required to Intune Lab Devices group
- [ ] Chrome auto-installed on enrolled devices
- [ ] App shows as installed in Company Portal

---

## Useful Links

| Resource | URL |
|---|---|
| Win32 Content Prep Tool | [github.com/microsoft/Microsoft-Win32-Content-Prep-Tool](https://github.com/microsoft/Microsoft-Win32-Content-Prep-Tool) |
| Chrome Enterprise download | [chromeenterprise.google/browser/download](https://chromeenterprise.google/browser/download/) |
| Intune Admin Centre | [intune.microsoft.com](https://intune.microsoft.com) |
| Win32 app deployment docs | [learn.microsoft.com/en-us/mem/intune/apps/apps-win32-app-management](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-app-management) |

---

*Previous: [04 · Configuration Profiles](../04-configuration-profiles/) · Next: [06 · Conditional Access](../06-conditional-access/)*