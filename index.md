---
layout: default
title: Privacy Policy
description: Privacy Policy for the Pocket Arcade mobile game.
permalink: /
---

# Privacy Policy

**Pocket Arcade**
**Effective date:** 14 June 2026
**Version:** 2.0 (full rewrite to reflect Build 41 architecture)
**Supersedes:** v1.0 (anonymous-on-device-only)

---

## 1. Overview

Pocket Arcade ("the app", "we", "us", "our") is a casual arcade game published
by the Pocket Arcade team. This policy explains what information we collect,
why we collect it, who we share it with, and your rights under India's
Digital Personal Data Protection Act 2023 (DPDP), the EU General Data
Protection Regulation (GDPR) and other applicable privacy laws.

From version 1.0.18 onwards, Pocket Arcade creates an **anonymous account
identifier** for every install so we can sync your progress across sessions
and devices, and so you can optionally link a Google account. This policy
describes how that identifier and any data attached to it are handled.

**In plain English:** we do not ask you to enter your name, phone number, or
location. We do create an anonymous device identifier on first launch, and
you may *choose* to link your Google account; both are described in
detail below.

## 2. Who we are

**Data Fiduciary** (DPDP §2(g)) /
**Data Controller** (GDPR Art. 4(7)):
Pocket Arcade team
Contact: pocketarcade.support@gmail.com

For DPDP grievance redressal (see §10), contact our Grievance Officer
at the same address with the subject line `DPDP Grievance — Pocket Arcade`.
We respond within 30 days (DPDP §13(2)).

## 3. What we collect

### 3.1 Identifiers automatically created on first launch
| Identifier | Where | Why |
|---|---|---|
| **Firebase Anonymous UID** | Google Firebase Authentication | Stable per-install identity that survives app upgrades. Lets us migrate progress when you link Google. |
| **Supabase User ID** | Supabase | Authoritative server identity for cloud save records. Distinct from the Firebase UID. |
| **Pocket Arcade Player ID** | On-device only (AsyncStorage) | Stable local identifier for offline-first features. Same value can be sent with pre-auth consent records. |
| **Android Advertising ID / Apple IDFA** | Google AdMob | Anonymous advertising identifier. You can reset or limit it at any time (see §6.2). |

### 3.2 Data you explicitly choose to provide
| Data | When | Where stored |
|---|---|---|
| **Google account email & display name** | If you tap **Sign In with Google** in Settings | Firebase Authentication; we store only the email, display name and the Google OpenID token reference |
| **Display name** edits | If you customise your profile | Supabase `profiles` table |

We **do not** request your phone number, physical address, contacts list,
camera, microphone, photo library, precise location, or any biometric data.

### 3.3 Game data we sync to the cloud
The app stores the following on your device (AsyncStorage) and, once consent
is given, mirrors them to Supabase cloud save so they survive a reinstall
and sync across devices that share the same Google account:

* Game progress: levels reached, modes unlocked
* Achievements & badges
* Coin balance and wallet history
* Settings (sound, music, haptics on/off)
* Daily Challenge submissions and streaks
* Statistics (best scores, total play time, lifetime aggregates)
* When the Daily Bundle Cloud Save flag is enabled, the Daily Bundle ledger
* When viral features are enabled, optional referral codes you generate or
  redeem, and any pending reward ledger entries

### 3.4 Diagnostics and telemetry (consent-gated)
With your consent (see §6) we collect:

* **Firebase Analytics** — gameplay events (session start, level complete,
  IAP purchased, rewarded-ad watched), device model and OS, coarse country.
  Events list is published in the in-app `View Privacy Policy` link.
* **Firebase Crashlytics** — crash stack traces, device model, OS, breadcrumbs
  emitted by Pocket Arcade code (no personal data). Crashlytics retention
  is 90 days (Firebase platform default).
* **Custom telemetry breadcrumbs** — server-side traces of cloud-save sync
  outcomes (success / fail), auth bootstrap outcomes, and viral attribution
  events (only when those features are enabled).

Telemetry is **disabled by default** on first launch. We do not log any
analytics event until you tap **Accept** on the in-app Privacy & Analytics
consent banner.

### 3.5 Audit & compliance records (always recorded)
For every account-affecting action — guest creation, Google sign-in,
consent acceptance, data export request, and account deletion request —
we write a server-timestamped row to a tamper-resistant `audit_events`
table on Supabase. These rows are:

* **Append-only** — neither you nor any client API can modify them.
* **Limited to closed-set event types** so we cannot use the table for
  arbitrary surveillance.
* **Visible to you** via *Export My Data* in Settings.
* **Retained for 365 days** then automatically purged.

### 3.6 In-app purchase records
If you purchase coins or remove ads, the Apple App Store or Google Play
handles your payment information. We **never** see your card number, billing
address, or payment method. We receive only the transaction identifier,
product SKU, and grant status, which we store in the `purchases` table to
prevent duplicate grants.

## 4. How we use the data

| Purpose | Legal basis (DPDP §6 / GDPR Art. 6) | What is processed |
|---|---|---|
| Sync your progress across sessions and devices | Consent (DPDP §6(1); GDPR 6(1)(a)) | Items in §3.3 |
| Detect and recover from crashes | Legitimate interest (GDPR 6(1)(f); DPDP exemption §17(2)(a) — research/statistics) | Items in §3.4 (Crashlytics only) |
| Improve gameplay through aggregated analytics | Consent (DPDP §6(1); GDPR 6(1)(a)) | Items in §3.4 (Analytics only); only after Accept |
| Show ads and rewarded videos to keep the game free | Consent (UMP banner) + legitimate interest for non-personalised | Items in §3.1 (ad ID); see §5 |
| Process IAP purchases | Contract performance (GDPR 6(1)(b)) | Items in §3.6 |
| Comply with deletion / export requests | Legal obligation (DPDP §11, §12) | Items in §3.5 |

## 5. Who we share data with

We share data with the following sub-processors, each of which is bound by
their own published data-processing agreement. No data is sold to any third
party.

| Sub-processor | Purpose | Data accessed | Privacy policy |
|---|---|---|---|
| **Google Firebase** (Google LLC) | Anonymous + Google authentication, Analytics, Crashlytics | Firebase UID, Google email/displayName, analytics events, crash traces | https://firebase.google.com/support/privacy |
| **Supabase** (Supabase Inc., AWS-hosted) | Cloud save, audit events, account deletion processing | Supabase user ID + all data in §3.3, §3.5, §3.6 | https://supabase.com/privacy |
| **Google AdMob** (Google LLC) | Banner, interstitial, rewarded-video advertising | Android Advertising ID / IDFA, IP, device data | https://policies.google.com/technologies/ads |
| **Google Sign-In** (Google LLC) | OAuth identity provider when you link Google | Google account email, display name, OpenID token | https://policies.google.com/privacy |
| **Apple App Store / Google Play** | Payment processing for IAP | Transaction receipts (we receive only the receipt ID and grant) | Apple Privacy Policy; Google Play Privacy Policy |

No data is transferred to any party outside this list. We do not engage
data brokers or marketing affiliates.

### 5.1 Cross-border transfers
Firebase and Supabase store data in AWS / Google Cloud regions outside
India. DPDP §16 currently permits transfer to any country not blacklisted
by the Central Government; we will update this section if the Government
issues a restricted-countries notification.

## 6. Your rights

### 6.1 Rights granted by law
| Right | DPDP § | GDPR Art. | How to exercise |
|---|---|---|---|
| Right of access | §11 | 15 | Settings → Account → **Export My Data** |
| Right to correction | §12 | 16 | Email pocketarcade.support@gmail.com |
| Right to erasure | §12 | 17 | Settings → Account → **Delete Account** (or by email) |
| Right to withdraw consent | §6(4) | 7(3) | Re-open Settings → tap **View Privacy Policy** → Withdraw Consent (Build 42+) |
| Right to grievance redressal | §13 | — | Email Grievance Officer at pocketarcade.support@gmail.com |
| Right to object to processing | — | 21 | Email us; we will stop within 30 days |
| Right to data portability | — | 20 | Export My Data returns standards-compliant JSON |

### 6.2 Advertising controls
* In-app UMP consent banner (first launch) — decline personalised ads.
* Android: Settings → Privacy → Ads → "Reset / Delete advertising ID".
* iOS: Settings → Privacy & Security → Apple Advertising → Personalised Ads = off.

### 6.3 Telemetry controls
Telemetry runs only after you tap **Accept** on the Privacy & Analytics
consent banner. Until then, no analytics event is sent. If you uninstall
the app, all on-device storage is removed by the operating system.

## 7. Retention

| Data category | Retained | How it ends |
|---|---|---|
| Active account records | Until you request deletion | Manual deletion request |
| Cloud-saved progress (cloud_save, leaderboard, achievements, purchases, daily bundle, viral) | Tied to the account; deleted by cascade when the account is deleted | Account deletion |
| **Audit events** | **365 days** | Daily `pg_cron` prune at 03:41 UTC |
| **Account deletion grace window** | **30 days** between request and hard purge | Hourly `pg_cron` purge job |
| `daily_bundle_audit` | 180 days | `pg_cron` prune |
| `viral_link_event` | 90 days | `pg_cron` prune (only when viral features enabled) |
| `viral_attribution` | 30 days | `pg_cron` prune (only when viral features enabled) |
| Firebase Crashlytics | 90 days | Firebase platform default |
| Firebase Analytics | 14 months | Firebase Console-configured default |
| In-app purchase receipts | Per Apple / Google policy (typically 7 years) | Out of our control; held by the platforms |

After the 30-day account-deletion grace window expires, a server-side
cron job purges your `auth.users` record. The DELETE cascades through
18 foreign-key relationships, wiping every owned row except for three
forensic audit rows (deletion-request, deletion-completed,
export-requested) whose `user_id` is nulled out and replaced with an
`archived_user_id` marker. Those three rows are retained for the 365-day
audit window.

## 8. Security

* All cloud writes are protected by Supabase Row-Level Security; you can
  only read or write rows owned by you.
* All audit-sensitive operations route through SECURITY DEFINER server-side
  functions; clients cannot directly INSERT, UPDATE, or DELETE audit data.
* Connections to Supabase and Firebase use HTTPS / TLS 1.2+.
* We do not store passwords (Google handles its own credentials).
* Service-role keys are held outside any client-reachable code path.

## 9. Children

The app is rated for general audiences. We do not knowingly collect
personal data from anyone under 13 (United States COPPA) or under 18
(India DPDP §9). If you believe a child has used the app without parental
consent, email us and we will delete the associated account within 7
days.

## 10. Grievance redressal (DPDP §13)

If you believe your DPDP rights have been violated, email our Grievance
Officer at pocketarcade.support@gmail.com with the subject line
`DPDP Grievance — Pocket Arcade`. We will respond within **30 days**.

If you are not satisfied with our response, you may register a complaint
with the Data Protection Board of India at
https://www.dpbi.gov.in (once operational; the Board is being constituted
as of June 2026).

## 11. Changes to this policy

We may update this policy. Material changes will:

1. Bump the `consent_version` constant in the app, which triggers a
   one-time Privacy & Analytics consent banner on next launch.
2. Be announced inside the app's Settings → View Privacy Policy link.
3. Be reflected in the **Effective date** at the top of this page.

You will not lose any data because of a policy update; we cannot start
collecting new categories of data without your fresh consent.

## 12. Contact

Pocket Arcade team
Email (Support + Privacy + Grievance): **pocketarcade.support@gmail.com**
Response time: 3 business days, 30 days max under DPDP §13.

To request export or deletion of your account, see the in-app Settings →
Account section, or our [Account & Data Deletion](./delete_account_v2.md) page.
