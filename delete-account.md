---
layout: default
title: Account & Data Deletion
description: Request deletion of your Pocket Arcade account and associated data.
permalink: /delete-account/
---

# Account & Data Deletion

**Pocket Arcade**
**Effective date:** 14 June 2026
**Version:** 2.0 (corrected to reflect Build 41 deferred-deletion architecture)
**Supersedes:** v1.0 (claimed immediate / 24-hour purge)

---

## 1. What this page is for

This page explains how to request deletion of your **Pocket Arcade**
account and all associated data, in line with India's Digital Personal
Data Protection Act 2023 (DPDP §12 — right of erasure),
Google Play's account-deletion policy, and Apple App Store guideline
5.1.1(v).

You can submit a deletion request from inside the app or by emailing
our support address. Both routes are described below.

## 2. Do you have an account?

| Pocket Arcade version | Account model |
|---|---|
| **1.0.17 and earlier** | Anonymous play. No account exists on our servers. Uninstall the app to remove local data. |
| **1.0.18 onwards** | Every install creates an anonymous Firebase account. You may optionally link Google. The steps below apply. |

Unsure which version you have? Open the app → **Settings** → scroll to the
bottom — the version appears under the app icon. When in doubt, proceed
with the request below; deletion is safe and idempotent.

## 3. Option A — Delete from inside the app (preferred)

1. Open **Pocket Arcade** on your device.
2. Tap the **Settings** icon from the main hub.
3. Scroll to the **ACCOUNT** section.
4. Tap **🗑 Delete Account**.
5. Read the irreversible-consequences notice.
6. Type `DELETE` in the confirmation field.
7. Tap **Delete Forever**.

The app will:

* Mark your account for deletion on our servers (a row is written to
  `account_deletion` and an `account_deletion_requested` audit row is
  recorded).
* Wipe all locally cached data from your device.
* Sign you out of Firebase and Supabase.
* Return you to the onboarding screen.

### What happens next

> **Important — deletion is not instant.**
> You will be signed out immediately, but your server data is held in a
> protected state for **30 days**. Final purge happens automatically at
> the end of that window, with no further action from you.

## 4. Option B — Request deletion by email

If you can no longer access the app (already uninstalled, lost device,
switched phones), email us and we will process your request manually.

Send an email to **pocketarcade.support@gmail.com** with the subject
line `Delete My Account — Pocket Arcade` and include:

* The email address linked to your Google sign-in *(or "guest" if you
  never linked Google)*
* Your display name in the app, if you set one
* Device type (iOS / Android) and approximate last-played date
* A confirmation that you are the account holder

We acknowledge within **3 business days** and complete deletion within
**30 days** of receipt. You will receive a confirmation email when
deletion completes.

## 5. The 30-day window — why it exists

We use a **30-day deferred deletion** model rather than an immediate
irreversible wipe because:

* It gives you a grace window in case the request was accidental or made
  under duress. (If you change your mind, email us within 30 days and we
  will cancel the request.)
* It satisfies the spirit of DPDP §10(1) which requires erasure within a
  "reasonable time" — 30 days is the industry standard and aligns with
  Google Play 2024 enforcement.
* It separates client-callable code from the privileged database action
  that actually deletes the `auth.users` row. The client never holds
  service-role keys; only a scheduled background job has erasure authority.

### Cancellation

To cancel a pending deletion within the 30-day window, email
pocketarcade.support@gmail.com with the subject
`Cancel Deletion — Pocket Arcade` from the email address linked to
your Google sign-in. We will remove the deletion marker manually.

*(A self-service cancellation button is planned for a future release;
this page will be updated when it ships.)*

## 6. Timeline

| Time | What happens |
|---|---|
| **T = 0** | You confirm deletion in the app (Option A) or send the email (Option B). |
| **T = 0** | A row is written to `account_deletion` with `scheduled_purge_at = T + 30 days`. An `account_deletion_requested` audit row is recorded with the server timestamp. |
| **T = 0** | Your local app data is wiped. You are signed out of Firebase and Supabase. |
| **T = 0 to T + 30 days** | Your server data exists in a sealed state. You cannot access it from the app. You may email to cancel. |
| **T + 30 days** | The hourly `account_deletion_purge` cron job processes your row. An `account_deleted` audit row is written. Your `auth.users` row is DELETEd. |
| **Cascade** | Every owned row across `profiles`, `cloud_save`, `leaderboard`, `purchases`, `daily_reward_claims`, `user_achievements`, `daily_bundle_claim`, `daily_bundle_audit`, `viral_code`, `viral_redemption`, `viral_link`, `viral_link_event`, `viral_attribution`, `viral_reward_ledger` is wiped by foreign-key `ON DELETE CASCADE`. |
| **T + 30 days** | Three forensic audit rows survive (`account_deletion_requested`, `account_deleted`, `data_export_requested`) with `user_id` nulled and `archived_user_id` stored in metadata. These exist for compliance audit trail. |
| **T + 365 days** | The daily `audit_events_prune` cron job deletes the three forensic rows. No trace of your account remains. |

## 7. What gets deleted

| Data type | When |
|---|---|
| Firebase Authentication record (anonymous or Google-linked) | T + 30 days |
| Supabase `auth.users` row | T + 30 days |
| Cloud-saved game progress (coins, achievements, leaderboards, daily bundle, statistics) | T + 30 days via FK cascade |
| `profiles` row (display name) | T + 30 days via FK cascade |
| Viral attribution / link / redemption / reward ledger rows owned by you | T + 30 days via FK cascade |
| Local app data on your device | T = 0 (immediately when you confirm in-app) |
| Audit events tied to your `user_id` (other than the three forensic rows) | T + 30 days via FK cascade |
| Forensic audit rows (deletion request, deletion completed, export requested) | T + 365 days |

## 8. What we retain (and why)

| Data | Retention | Why |
|---|---|---|
| Aggregated, anonymised analytics aggregates that contain no user identifier | Indefinite | Cannot be used to identify you; helps us improve the game. |
| Firebase Crashlytics traces | 90 days | Cannot be used to re-identify you; auto-purged. |
| In-app purchase receipts | Per Apple / Google retention (~ 7 years) | We do not control; held by the platforms for tax & finance reasons. |
| Support correspondence | 12 months | Quality assurance; auto-deleted after 12 months. |
| Three forensic audit rows | 365 days | DPDP §17 audit trail requirement. |
| Records required by law enforcement | Only if a valid request was received before deletion | Otherwise: none. |

Note: if you want **Apple** or **Google** to delete data they hold about
you (e.g. purchase history, ad ID, Firebase Analytics ID at the platform
level), you must contact those companies directly.

## 9. Need help?

Email **pocketarcade.support@gmail.com** — we respond within 3 business
days.

For DPDP-specific grievances, use the subject line
`DPDP Grievance — Pocket Arcade`. We will respond within 30 days
as required by DPDP §13(2).
