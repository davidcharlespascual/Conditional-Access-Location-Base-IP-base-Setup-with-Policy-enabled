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

![Overview Screenshot](image_139ed8.png)

---

## Part 1: IP-Based Policy (Require MFA outside Home Lab)

### Step 1: Configuring Named Locations (IP Ranges)
We set up a trusted IP range representing the homelab network in the Entra admin center.
![Conditional Access IP Base](conditional%20access%20ip%20base.jpg)

### Step 2: Refining IP Range Properties
Reviewing and saving the IPv4/IPv6 range configuration and marking it as a trusted location (`Homelab - lab -globe`).
![Conditional Access IP Base 2](conditional%20access%20ip%20base%202.jpg)

### Step 3: Creating the Conditional Access Policy
Creating a new policy named **"Require MFA outside Home Lab"** to target cloud resources and assign conditions based on network locations.
![Policy for IP Base Access](policy%20for%20ipBase%20access.jpg)

### Step 4: Configuring Exclusions for Trusted Locations
Configuring the policy settings to exclude the trusted `Homelab - lab - globe` location so that users inside the home network bypass external MFA triggers.
![Settings for IP Blocking](settings%20for%20ipBlocking.jpg)

### Step 5: Testing with Report-Only Mode
Verifying that the IP-based policy works as expected by checking the **Report-only** tab in sign-in activity details.
![Confirming IP Policy under Report Only Tab](confirming%20ip%20policy%20is%20working%20under%20report%20only%20tab.jpg)

### Step 6: Successful Sign-in within Home Network
Reviewing sign-in events to confirm successful authentication when the user's IP address falls within the trusted home range.
![IP is within home range successful signin](ip%20is%20within%20home%20range%20successed%20signin.jpg)

### Step 7: Confirmation of Access
Confirming that the user can successfully sign out and access their mailbox within the home network without unnecessary blocks.
![Confirmation she can sign out within home network](confirmation%20she%20can%20signout%20within%20home%20network%20no%20mfa%20required.jpg)

---

## Part 2: Location-Based Policy (Block access outside the Philippines)

### Step 1: Reviewing Active Location Policies
Reviewing active user-created policies in Microsoft Entra ID, specifically the **"Blocked access outside philippines_ITGroup"** policy.
![Testing Conditional Policies Blocking Access Outside Philippines](testing%20%20Conditional%20policies%20Blocking%20access%20outside%20Philippines.jpg)

### Step 2: Policy Evaluation Results & What-If Testing
Checking policy evaluation results and using the **What If** tool to test conditions (such as device platform, browser, simulated IP address, and country).
![Testing China Location](testing%20china%20location.jpg)

### Step 3: Testing Specific Cloud Apps
Targeting specific cloud applications like **Office 365 Exchange Online** in the What If simulation tool to see policy impact.
![Testing Exchange Online if user can sign in](testing%20exchange%20online%20if%20user%20cansignin.jpg)

### Step 4: Simulating External Access with VPN
Using Proton VPN to connect to an external server (such as Japan) to test real-world geo-blocking behavior.
![Testing Using VPN](testing%20using%20vpn.jpg)

### Step 5: User Access Blocked by Entra ID
Verifying that Entra ID successfully detects the foreign VPN IP address (Japan) and blocks user access as mandated by the policy.
![User Blocked Entra Detected Japan IP Here](user%20blocked%20entra%20detected%20japan%20IP%20here.jpg)

### Step 6: Investigating Sign-in Logs
Investigating sign-in logs when a user attempts to log in from Minato-Ku, Tokyo, resulting in failure entries.
![Sign-in Logs shows user try to log in Tokyo](signin%20Logs%20shows%20user%20try%20to%20log%20in%20tokyo.jpg)

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
