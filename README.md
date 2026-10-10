# Conditional Access Lab: IP-Based and Location-Based Policies in Microsoft Entra ID

Two hands-on Conditional Access exercises in my home lab tenant. The first requires MFA whenever a user signs in from anywhere other than my trusted home network (IP-based). The second blocks sign-ins from outside the Philippines (location-based). Both were built, simulated, and tested with real sign-ins.

> **Note:** This is a lab environment. All accounts, groups, and policies belong to a test tenant, and all sign-in tests used test users.

---

## Contents

* Overview
* Starting Point
* Part 1: IP-Based Policy (Require MFA outside Home Lab)
* Part 2: Location-Based Policy (Block access outside the Philippines)
* What I've Learned
* Troubleshooting
* Next Steps
* Skills Demonstrated

---

## Overview

| Category | Details |
| :--- | :--- |
| **Goal** | Control where users can sign in from, using Conditional Access |
| **Platform** | Microsoft Entra ID, Conditional Access |
| **Tenant** | evilcorpLAB (lab tenant) |
| **Policy 1** | Require MFA outside Home Lab (IP-based, report-only) |
| **Policy 2** | Blocked access outside philippines_ITGroup (location-based, On) |
| **Test users** | Carmina Galvelo (IT), jaydee mamba |
| **Testing tools** | What If tool, Sign-in logs, report-only results, Proton VPN, InPrivate browser sessions |

---

## Starting Point

Before building anything, I reviewed what the tenant already enforced. Security defaults cannot be enabled here, because the tenant already contains custom user-created policies.

<img src="image_139ed8.png" alt="Overview Screenshot" width="800">

---

## Part 1: IP-Based Policy (Require MFA outside Home Lab)

### Step 1: Configuring Named Locations (IP Ranges)
We set up a trusted IP range representing the homelab network in the Entra admin center[cite: 21, 22].
<img src="conditional%20access%20ip%20base_2.jpg" alt="Conditional Access IP Base" width="800">

### Step 2: Refining IP Range Properties
Reviewing and saving the IPv4/IPv6 range configuration and marking it as a trusted location (`Homelab - lab -globe`)[cite: 21].
<img src="conditional%20access%20ip%20base%202_2.jpg" alt="Conditional Access IP Base 2" width="800">

### Step 3: Creating the Conditional Access Policy
Creating a new policy named **"Require MFA outside Home Lab"** to target cloud resources and assign conditions based on network locations[cite: 26].
<img src="policyforipBase%20access.jpg" alt="Policy for IP Base Access" width="800">

### Step 4: Configuring Exclusions for Trusted Locations
Configuring the policy settings to exclude the trusted `Homelab - lab - globe` location so that users inside the home network bypass external MFA triggers[cite: 28].
<img src="settingsforip%20blocking.jpg" alt="Settings for IP Blocking" width="800">

### Step 5: Testing with Report-Only Mode
Verifying that the IP-based policy works as expected by checking the **Report-only** tab in sign-in activity details[cite: 24].
<img src="confirming%20ip%20policy%20is%20working%20under%20report%20only%20tab_2.jpg" alt="Confirming IP Policy under Report Only Tab" width="800">

### Step 6: Successful Sign-in within Home Network
Reviewing sign-in events to confirm successful authentication when the user's IP address falls within the trusted home range[cite: 25].
<img src="ipiswithinhome%20rangesuccessed%20signin.jpg" alt="IP is within home range successful signin" width="800">

### Step 7: Confirmation of Access
Confirming that the user can successfully sign out and access their mailbox within the home network without unnecessary blocks[cite: 23].
<img src="confirmation%20she%20can%20signout%20within%20home%20network%20no%20mfa%20required_2.jpg" alt="Confirmation she can sign out within home network" width="800">

---

## Part 2: Location-Based Policy (Block access outside the Philippines)

### Step 1: Reviewing Active Location Policies
Reviewing active user-created policies in Microsoft Entra ID, specifically the **"Blocked access outside philippines_ITGroup"** policy[cite: 29, 31].
<img src="showingpolicy%20locationbase%20blocking.jpg" alt="Showing Policy Location Base Blocking" width="800">

### Step 2: Active Policy Overview
Confirming the enabled location-based policy configured to block traffic outside the allowed region[cite: 31].
<img src="testing%20%20Conditional%20policies%20Blocking%20access%20outside%20Philippines_2.jpg" alt="Testing Conditional Policies Blocking Access Outside Philippines" width="800">

### Step 3: Policy Evaluation Results
Checking policy evaluation results to verify which controls apply to targeted user accounts[cite: 27].
<img src="result_2.jpg" alt="Result" width="800">

### Step 4: What-If Simulation for Specific Countries
Using the **What If** tool to simulate a sign-in attempt originating from China using a test IP address (`114.114.114.114`)[cite: 32].
<img src="testingchina%20location.jpg" alt="Testing China Location" width="800">

### Step 5: What-If Simulation for Target Cloud Apps
Selecting specific applications such as **Office 365 Exchange Online** in the What If simulation tool to check policy enforcement[cite: 33].
<img src="testingexchange%20onlineifusercan%20signin.jpg" alt="Testing Exchange Online if user can sign in" width="800">

### Step 6: Simulating External Access with VPN
Using Proton VPN connected to a server in Japan (`159.26.119.227`) to perform a real-world test of the geo-blocking rule[cite: 34].
<img src="testingusing%20vpn.jpg" alt="Testing Using VPN" width="800">

### Step 7: Real User Access Blocked by Entra ID
Confirming that Microsoft Entra ID intercepts the user sign-in from Japan and displays the **"You cannot access this right now"** block screen[cite: 35].
<img src="userblockedentra%20detectedjapanIP%20here.jpg" alt="User Blocked Entra Detected Japan IP Here" width="800">

### Step 8: Investigating Sign-in Logs
Reviewing the user sign-in logs to verify failed login attempts originating from Minato-Ku, Tokyo, matching the blocked policy trigger[cite: 30].
<img src="signinLogsshows%20usertrytologin%20tokyo.jpg" alt="Sign-in Logs shows user try to log in Tokyo" width="800">

---

## What I've Learned
Through these labs, I gained hands-on experience in securing organizational resources using Microsoft Entra ID Conditional Access policies. Key takeaways include:
* **Named Locations:** How to define specific IP ranges (trusted homelabs) and geographic regions (countries) to manage network-based access rules.
* **Policy Enforcement & Report-Only Mode:** Testing policies safely using Report-Only mode to verify their impact before enforcing them on users.
* **Sign-in Logs & Troubleshooting:** Analyzing real-time user sign-in events to confirm whether access was granted, interrupted, or successfully blocked based on location and IP criteria.

---

## Troubleshooting
* **Report-Only Insights:** Utilizing the Report-Only feature ensures rules can be evaluated safely against live traffic before switching them to "On".
* **VPN Verification:** When testing geo-blocking, make sure your VPN client is active and verify the assigned public IP address matches your testing region.

---

## Next Steps
* Expand Conditional Access coverage to mobile device management (Intune) compliance policies.
* Implement Risk-Based Conditional Access policies for user and sign-in risk detection.

---

## Skills Demonstrated
* Microsoft Entra ID Administration
* Conditional Access Policy Creation & Testing
* Named Locations & Geo-Fencing Configuration
* Security Log Analysis & Troubleshooting
