# Conditional Access Lab: IP-Based and Location-Based Policies in Microsoft Entra ID

Two hands-on Conditional Access exercises in my home lab tenant. The first requires MFA whenever a user signs in from anywhere other than my trusted home network (IP-based). The second blocks sign-ins from outside the Philippines (location-based). Both were built, simulated, and tested with real sign-ins.

> **Note:** This is a lab environment. All accounts, groups, and policies belong to a test tenant, and all sign-in tests used test users.

---

## Contents

- [Overview](#overview)
- [Starting Point](#starting-point)
- [Part 1: IP-Based Policy (Require MFA outside Home Lab)](#part-1-ip-based-policy-require-mfa-outside-home-lab)
- [Part 2: Location-Based Policy (Block access outside the Philippines)](#part-2-location-based-policy-block-access-outside-the-philippines)
- [Comparing the Two Policies](#comparing-the-two-policies)
- [What I've Learned](#what-ive-learned)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)
- [Skills Demonstrated](#skills-demonstrated)

---

## Overview

| | |
|---|---|
| **Goal** | Control where users can sign in from, using Conditional Access |
| **Platform** | Microsoft Entra ID, Conditional Access |
| **Tenant** | evilcorpLAB (lab tenant) |
| **Policy 1** | Require MFA outside Home Lab (IP-based, report-only) |
| **Policy 2** | Blocked access outside philippines_ITGroup (location-based, On) |
| **Test users** | Carmina Galvelo (IT), jaydee mamba |
| **Testing tools** | What If tool, Sign-in logs, report-only results, Proton VPN, InPrivate browser sessions |

## Starting Point

Before building anything, I reviewed what the tenant already enforced. Security defaults cannot be enabled here, because the tenant already uses Conditional Access policies. Four **Microsoft-managed policies** were already On:

- Block legacy authentication
- Multifactor authentication for Azure Management
- Multifactor authentication for admins
- Multifactor authentication for all users

That meant "require MFA for everyone" and "block legacy auth" were already covered, so I built policies that
