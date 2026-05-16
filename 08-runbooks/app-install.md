# Runbook — Cannot Install an Application

## Scenario
A user cannot install an application they need for work. They are downloading it from the internet and getting a permissions error.

---

## Steps

### 1. Identify the Application
Ask the user what application they are trying to install. You need to know what it is before taking any action.

### 2. Check if it is an Approved Application
Before doing anything else, check whether the application is on the organisation's approved software list. Not every application a user wants is one they should have.

- If it is not approved — inform the user and advise them to raise a request through the appropriate channel (manager approval, software request form etc). Do not deploy unapproved software.
- If it is approved — continue below.

### 3. Check Company Portal
Ask the user to open Company Portal on their device. The application may already be available there as an **Available** app, meaning they need to install it manually from the portal rather than from the internet.

### 4. Check Intune for Existing Deployment
[intune.microsoft.com](https://intune.microsoft.com) → **Apps** → **All apps** → search for the application

- Is it deployed? If yes, check the assignment:
  - Is the user's group included?
  - Is the user's group accidentally excluded?

### 5. Check Entra ID Group Membership
[entra.microsoft.com](https://entra.microsoft.com) → **Users** → select the user → **Groups** → confirm they are in the group the app is assigned to.

If they are not in the correct group, add them and force a sync on the device.

### 6. If the App is Not Deployed
1st line typically does not package and deploy new applications independently. Raise a request with 2nd line or IT ops to:
- Package the application using the Win32 Content Prep Tool
- Upload and configure it in Intune
- Assign it to the appropriate group

Once deployed, add the user to the relevant group.

---

## Escalate If
- The application is not on the approved software list — do not deploy, advise the user to raise a formal request
- The application needs to be packaged and added to Intune — raise a request with 2nd line or IT ops
- The app is deployed but failing to install on the device — check the app installation status in Intune and escalate if errors are present

---

## Notes
- The permissions error the user is seeing is Intune working correctly — standard users cannot install software without admin rights, which is intentional. Reassure the user their device is not faulty
- Always verify the app is approved before taking action — this protects you and the organisation
- If the app is in Company Portal as Available rather than Required, walk the user through installing it from there rather than raising a new deployment request
