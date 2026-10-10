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

![Overview Screenshot](image_139ed8.png)

---

## Part 1: IP-Based Policy (Require MFA outside Home Lab)

### Step 1: Configuring Named Locations (IP Ranges)
We set up a trusted IP range representing the homelab network in the Entra admin center.
![Conditional Access IP Base](conditional access ip base_2.jpg)

### Step 2: Refining IP Range Properties
Reviewing and saving the IPv4/IPv6 range configuration and marking it as a trusted location (`Homelab - lab -globe`).
![Conditional Access IP Base 2](conditional access ip base 2_2.jpg)

### Step 3: Creating the Conditional Access Policy
Creating a new policy named **"Require MFA outside Home Lab"** to target cloud resources and assign conditions based on network locations.
![Policy for IP Base Access](policyforipBase access.jpg)

### Step 4: Configuring Exclusions for Trusted Locations
Configuring the policy settings to exclude the trusted `Homelab - lab - globe` location so that users inside the home network bypass external MFA triggers.
![Settings for IP Blocking](settingsforip blocking.jpg)

### Step 5: Testing with Report-Only Mode
Verifying that the IP-based policy works as expected by checking the **Report-only** tab in sign-in activity details.
![Confirming IP Policy under Report Only Tab](confirming ip policy is working under report only tab_2.jpg)

### Step 6: Successful Sign-in within Home Network
Reviewing sign-in events to confirm successful authentication when the user's IP address falls within the trusted home range.
![IP is within home range successful signin](ipiswithinhome rangesuccessed signin.jpg)

### Step 7: Confirmation of Access
Confirming that the user can successfully sign out and access their mailbox within the home network without unnecessary blocks.
![Confirmation she can sign out within home network](confirmation she can signout within home network no mfa required_2.jpg)

---

## Part 2: Location-Based Policy (Block access outside the Philippines)

### Step 1: Reviewing Active Location Policies
Reviewing active user-created policies in Microsoft Entra ID, specifically the **"Blocked access outside philippines_ITGroup"** policy.
![Showing Policy Location Base Blocking](showingpolicy locationbase blocking.jpg)

### Step 2: Active Policy Overview
Confirming the enabled location-based policy configured to block traffic outside the allowed region.
![Testing Conditional Policies Blocking Access Outside Philippines](testing  Conditional policies Blocking access outside Philippines_2.jpg)

### Step 3: Policy Evaluation Results
Checking policy evaluation results to verify which controls apply to targeted user accounts.
![Result](result_2.jpg)

### Step 4: What-If Simulation for Specific Countries
Using the **What If** tool to simulate a sign-in attempt originating from China using a test IP address (`114.114.114.114`).
![Testing China Location](testingchina location.jpg)

### Step 5: What-If Simulation for Target Cloud Apps
Selecting specific applications such as **Office 365 Exchange Online** in the What If simulation tool to check policy enforcement.
![Testing Exchange Online if user can sign in](testingexchange onlineifusercan signin.jpg)

### Step 6: Simulating External Access with VPN
Using Proton VPN connected to a server in Japan (`159.26.119.227`) to perform a real-world test of the geo-blocking rule.
![Testing Using VPN](testingusing vpn.jpg)

### Step 7: Real User Access Blocked by Entra ID
Confirming that Microsoft Entra ID intercepts the user sign-in from Japan and displays the **"You cannot access this right now"** block screen.
![User Blocked Entra Detected Japan IP Here](userblockedentra detectedjapanIP here.jpg)

### Step 8: Investigating Sign-in Logs
Reviewing the user sign-in logs to verify failed login attempts originating from Minato-Ku, Tokyo, matching the blocked policy trigger.
![Sign-in Logs shows user try to log in Tokyo](signinLogsshows usertrytologin tokyo.jpg)

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
