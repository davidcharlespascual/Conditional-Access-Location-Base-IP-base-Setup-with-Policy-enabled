# Conditional Access Lab: IP-Based and Location-Based Policies in Microsoft Entra ID

Two hands-on Conditional Access exercises in my home lab tenant. The first requires MFA whenever a user signs in from anywhere other than my trusted home network (IP-based). The second blocks sign-ins from outside the Philippines (location-based). Both were built, simulated, and tested with real sign-ins.

> **Note:** This is a lab environment. All accounts, groups, and policies belong to a test tenant, and all sign-in tests used test users.

---

## Contents

* Overview
* Starting Point
* Part 1: IP-Based Policy (Require MFA outside Home Lab)
* Part 2: Location-Based Policy (Block access outside the Philippines)
* Comparing the Two Policies
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
We set up a trusted IP range representing the homelab network in the Entra admin center.
<img src="conditional access ip base.jpg" alt="Conditional Access IP Base" width="800">

### Step 2: Refining IP Range Properties
Reviewing and saving the IPv4/IPv6 range configuration and marking it as a trusted location (`Homelab - lab -globe`).
<img src="conditional access ip base 2.jpg" alt="Conditional Access IP Base 2" width="800">

### Step 3: Creating the Conditional Access Policy
Creating a new policy named **"Require MFA outside Home Lab"** to target cloud resources and assign conditions based on network locations.
<img src="policy for ipBase access.jpg" alt="Policy for IP Base Access" width="800">

### Step 4: Configuring Exclusions for Trusted Locations
Configuring the policy settings to exclude the trusted `Homelab - lab - globe` location so that users inside the home network bypass external MFA triggers.
<img src="settings for ipBlocking.jpg" alt="Settings for IP Blocking" width="800">

### Step 5: Testing with Report-Only Mode
Verifying that the IP-based policy works as expected by checking the **Report-only** tab in sign-in activity details.
<img src="confirming ip policy is working under report only tab.jpg" alt="Confirming IP Policy under Report Only Tab" width="800">

### Step 6: Successful Sign-in within Home Network
Reviewing sign-in events to confirm successful authentication when the user's IP address falls within the trusted home range.
<img src="ip is within home range successed signin.jpg" alt="IP is within home range successful signin" width="800">

### Step 7: Confirmation of Access
Confirming that the user can successfully sign out and access their mailbox within the home network without unnecessary blocks.
<img src="confirmation she can signout within home network no mfa required.jpg" alt="Confirmation she can sign out within home network" width="800">

---

## Part 2: Location-Based Policy (Block access outside the Philippines)

### Step 1: Reviewing Active Location Policies
Reviewing active user-created policies in Microsoft Entra ID, specifically the **"Blocked access outside philippines_ITGroup"** policy.
<img src="testing  Conditional policies Blocking access outside Philippines.jpg" alt="Testing Conditional Policies Blocking Access Outside Philippines" width="800">

### Step 2: Policy Evaluation Results & What-If Testing
Checking policy evaluation results and using the **What If** tool to test conditions (such as device platform, browser, simulated IP address, and country).
<img src="testing china location.jpg" alt="Testing China Location" width="800">

### Step 3: Testing Specific Cloud Apps
Targeting specific cloud applications like **Office 365 Exchange Online** in the What If simulation tool to see policy impact.
<img src="testing exchange online if user cansignin.jpg" alt="Testing Exchange Online if user can sign in" width="800">

### Step 4: Simulating External Access with VPN
Using Proton VPN to connect to an external server (such as Japan) to test real-world geo-blocking behavior.
<img src="testing using vpn.jpg" alt="Testing Using VPN" width="800">

### Step 5: User Access Blocked by Entra ID
Verifying that Entra ID successfully detects the foreign VPN IP address (Japan) and blocks user access as mandated by the policy.
<img src="user blocked entra detected japan IP here.jpg" alt="User Blocked Entra Detected Japan IP Here" width="800">

### Step 6: Investigating Sign-in Logs
Investigating sign-in logs when a user attempts to log in from Minato-Ku, Tokyo, resulting in failure entries.
<img src="signin Logs shows user try to log in tokyo.jpg" alt="Sign-in Logs shows user try to log in Tokyo" width="800">

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
