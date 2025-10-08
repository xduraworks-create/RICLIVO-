---

## 📱 **File 2: onboarding_screen.md**

```markdown
# Riclivo Onboarding Screen Documentation

This document describes the onboarding process for new users — ensuring a smooth and compliant registration flow across countries and platforms.

---

## 1. Overview

The onboarding flow introduces Riclivo’s key benefits while ensuring KYC and compliance data are securely captured before account activation.

---

## 2. Step-by-Step Onboarding Flow

| Step | Screen | Description | Key Action |
|------|---------|--------------|-------------|
| **1** | Welcome Screen | Riclivo logo + tagline: *“Smarter finance. Real refunds. Total control.”* | “Get Started” button |
| **2** | Sign-up Options | Choose sign-up via Email, Google, or Phone | `POST /auth/register` |
| **3** | KYC Prompt | Collects name, ID, and basic address | `POST /auth/kyc` |
| **4** | Choose Account Type | Personal / Business | Sets user role in DB |
| **5** | Wallet Setup | Creates Riclivo wallet in user’s currency | `/wallet/create` |
| **6** | AI Chat Intro | Short animation introducing the AI finance assistant | Starts AI onboarding |
| **7** | Data Consent | Displays GDPR & Privacy Policy checkbox | `POST /user/consent` |
| **8** | Dashboard Launch | Redirect to main app dashboard | Loads user data |

---

## 3. Visual Flow (Text Layout)

```plaintext
Welcome → Sign-up → KYC → Select Type → Wallet Setup → AI Chat Intro → Consent → Dashboard
