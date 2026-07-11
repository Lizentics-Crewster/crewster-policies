---
title: Crewster — Privacy Policy
permalink: /privacy-policy/
---

# Crewster — Privacy Policy

**Last updated**: 2026-07-11

---

## Summary (TL;DR)

- **Your roster data NEVER leaves your device.** Imported PDFs and every duty
  parsed from them live only in on-device SQLite (WatermelonDB) + the app sandbox.
  There is no server-side roster database. *Evidence*: `src/services/data-export.ts`
  `buildExportPayload` queries only local WMDB collections; no roster upload path
  exists anywhere in `src/services/`.
- **Account email is the only personal data stored off-device.** Held by Supabase
  Auth for sign-in. *Evidence*: `src/services/supabase-client.ts`;
  `src/services/auth.ts` (`signUp`/`signIn` call `supabase.auth.*`, no server-side
  profile writes).
- **Anonymous crash reports** go to Sentry, opt-out. *Evidence*:
  `src/services/telemetry-sentry.ts` (`initTelemetry`, `beforeSend` PII scrub,
  `setUser({ id })` UUID-only).
- **No ads, no analytics SDKs, no device identifiers, no location.** *Evidence*:
  no analytics dependency in `package.json`; `Sentry.init` `tracesSampleRate: 0`.

---

## 1. Data controller

Crewster is operated by **Lizentics Talent FZE**, a Free Zone Establishment
registered in **Ajman, United Arab Emirates** ("Lizentics", "we", "us").
Contact: `devsupport@lizentics.com`.

Crewster is available to users **worldwide**. Where the EU General Data Protection
Regulation (Regulation (EU) 2016/679, "GDPR") applies to a user (users in the EU/EEA),
Lizentics acts as **controller** for the personal data described below and grants the
GDPR rights in Section 5. The UK GDPR is honoured on the same terms for UK users.

> `[DECISIÓN GERARDO — EU representative]` Because the controller is established
> **outside** the EU yet offers the app to EU/EEA data subjects, **GDPR Art. 27**
> normally requires a designated EU representative (a named person/entity in an
> EU member state), and **Art. 13(1)(a)** requires publishing their identity +
> contact here. Two exceptions may remove the obligation: (a) processing is
> occasional AND does not include large-scale special-category data AND is unlikely
> to risk rights/freedoms; (b) a public authority. Crewster's processing (email +
> pseudonymous UUID + crash diagnostics) is arguably low-risk, but "occasional" is
> unlikely to hold for a standing user base. **Recommendation**: appoint an EU
> representative (services from ~€100–300/yr) and add their name + address here
> before EU launch, OR obtain a documented legal opinion that the Art. 27 exception
> applies. Tracked in `docs/store/release-readiness-report.md`
> → `[DECISIONES GERARDO PENDIENTES]`.

## 2. What we collect

### 2.1 Email + password (authentication) — OFF-DEVICE

Stored by **Supabase Auth** (Supabase Inc.). *Evidence*:
`src/services/supabase-client.ts`; `src/services/auth.ts`
`signUp`/`signIn`/`requestPasswordReset`/`verifyOtp`/`resendOtp`.
Purposes: identify the account across devices/reinstalls; deliver the sign-up and
password-reset 6-digit OTP codes.
**Legal basis (GDPR, EU users)**: Art. 6(1)(b) — performance of a contract (no app
use without an account).

### 2.2 Pseudonymous account UUID — OFF-DEVICE (linked to crash reports)

The Supabase Auth UUID is attached to crash reports so distinct users hitting a bug
can be counted. **Never the email.** *Evidence*: `telemetry-sentry.ts` `setUser` —
`Sentry.setUser({ id: user.id })`; `beforeSend` force-drops `event.user` to `{ id }`.

### 2.3 Roster + logbook data — ON-DEVICE ONLY

Imported PDFs live in the app sandbox; parsed activities, day summaries, logbook
entries, aircraft/FSTD registries, pay-rate inputs, preferences and the change trace
live in local SQLite. *Evidence*: the full local schema enumerated by
`data-export.ts` `ExportPayload` (`roster_imports`, `activities`, `logbook_entries`,
`aircraft`, `fstd_devices`, `user_rates`, `user_preferences`, `trash_items`,
`activity_changes`, …). None have a server write path.
**Optional profile name + phone** (`saveUserProfile`/`updateUserProfileFields` in
`src/services/user-profile.ts`) are written to the local `users` row only — never
sent to Supabase.
**Logbook photo attachments** (scanned documents + MCDU photos) are stored as local
files (`src/components/logbook/EntryDocuments.tsx` `launchImageLibraryAsync`,
`FlightEditorScreen.tsx` `launchCameraAsync`; `src/services/attachments.ts`) — never
uploaded.

### 2.4 Anonymous crash reports — OFF-DEVICE (opt-out)

Sent to **Sentry** (Functional Software Inc.) on unhandled production errors.
Default enabled (`user_preferences.crash_reports_enabled`, legitimate-interest
default per D-39). Contents: stack trace, breadcrumbs, device model/OS/app-version/
memory, and the pseudonymous UUID.
*Evidence*: `telemetry-sentry.ts` — `initTelemetry` (skips under `__DEV__`, skips
when `opted === false`, skips with no DSN); `captureError`; the `beforeSend` scrub
battery (`scrubString`/`scrubDeep` from `src/utils/pii-scrub.ts`) applied to
message/exception/contexts/tags/extra/user/request/transaction/fingerprint/
breadcrumbs; `beforeBreadcrumb` drops `console` breadcrumbs.
**Never in a crash report**: email, password, JWT, roster content, typed input
(force-scrubbed at `beforeSend`).
**Legal basis (GDPR, EU users)**: Art. 6(1)(f) — legitimate interest in stability;
opt-out via Settings → Privacy and Security → Crash reports.

## 3. Sub-processors

| Sub-processor | Receives | Region | Legal basis (EU users) |
| --- | --- | --- | --- |
| Supabase Inc. | Email + password hash + account UUID | EU (Frankfurt) `[UNVERIFIED — confirm project region in Supabase dashboard; prod ref `gzmwcbtrxbgmkvvwqqii`]` | Art. 6(1)(b) |
| Functional Software Inc. (Sentry) | Anonymous crash reports + UUID | EU `[UNVERIFIED — confirm Sentry org region + EU Data Residency add-on; org `lizentics-talent`, `eas.json` `SENTRY_ORG`]` | Art. 6(1)(f) |

Both bound by GDPR DPAs. `[DECISIÓN GERARDO: confirm DPAs signed before publish.]`
Because the controller is in the UAE, personal data may be processed under the
sub-processors' EU infrastructure and accessed from the UAE; the appropriate transfer
mechanism (SCCs / adequacy) is `[DECISIÓN GERARDO — confirm with the DPAs]`.

## 4. We do NOT collect

- No advertising identifiers (no IDFA/IDFV/AAID). *Evidence*: no tracking SDK in
  `package.json`; no ATT string configured.
- No location. *Evidence*: no location permission in `AndroidManifest.xml`; no
  `NSLocation*` key requested by any config plugin in `app.config.js`.
- No product analytics (no PostHog/Mixpanel/GA/Firebase/Amplitude in `package.json`).
- No contacts / no SMS / no microphone-recorded audio (see
  `docs/store/permissions-justification.md`).

## 5. Your rights

### 5.1 GDPR rights (EU/EEA users; UK GDPR equivalent for UK users) — Art. 15–22

- **Access / rectification** (15/16): via `devsupport@lizentics.com`.
- **Erasure** (17): Settings → Privacy and Security → **Delete my account** —
  server-side deletion via the `delete-user` Supabase Edge Function
  (`supabase/functions/delete-user`; invoked by `auth.ts` `deleteAccount`,
  `verify_jwt: true`), then a full local wipe (`erase-user-local-data.ts`
  `eraseAllUserLocalData` — activities, roster imports + PDFs, logbook, aircraft/FSTD,
  attachments + signature files, preferences, rates, the 30-day trash, the change
  trace, and the materialised `calendar_state`), then sign out. Rosters alone can be
  wiped without deleting the account via Settings → Delete all imported rosters
  (`reset-roster-data.ts`).
- **Portability** (20): Settings → Privacy and Security → **Export my data** — a JSON
  dump of every local table for the user (`data-export.ts` `exportUserData`,
  wired in `src/app/(app)/(tabs)/settings/security.tsx`; `EXPORT_FORMAT_VERSION = 8`).
  PDF binaries are excluded (the user still has them in their email); `raw_text` of
  each roster IS included.
- **Object** (21): opt out of crash reports (Settings → Privacy and Security →
  Crash reports).

We respond within 30 days (Art. 12(3)). EU users may lodge a complaint with their
national supervisory authority (find yours at
`https://edpb.europa.eu/about-edpb/about-edpb/members_en`).

### 5.2 Users outside the EU/EEA/UK

All users worldwide can exercise the same practical controls in-app (delete account,
export data, opt out of crash reports) and by emailing `devsupport@lizentics.com`,
regardless of whether GDPR applies to them.

## 6. Security

- **In transit**: HTTPS/TLS to Supabase + Sentry. `app.config.js`
  `ios.infoPlist.ITSAppUsesNonExemptEncryption = false` (standard HTTPS only, no
  custom crypto). No network call carries roster bytes.
- **At rest**: OS-level encryption (iOS Data Protection / Android FBE), gated by the
  device passcode. Auth session in `expo-secure-store` (iOS Keychain / Android
  Keystore) written with `AFTER_FIRST_UNLOCK_THIS_DEVICE_ONLY` so the JWT does NOT
  replicate via encrypted iCloud Keychain backups. *Evidence*: `supabase-client.ts`
  `ChunkedSecureStoreAdapter.setItem`. Android manifest restricts backup
  (`@xml/secure_store_backup_rules` / `@xml/secure_store_data_extraction_rules`).
  **A device without a passcode/PIN/biometric is NOT encrypted at rest** — a platform
  limitation, not a Crewster choice. SQLCipher per-row encryption is deferred to v2
  (see `CLAUDE.md` stack rationale).
- **Your responsibility**: set a device passcode; keep your account password secret
  (Crewster never asks for it outside sign-in / change-password).
- **Breach notification**: where GDPR applies, within 72 h of awareness (Art. 33/34)
  via in-app banner + email. `[DECISIÓN GERARDO: confirm the in-app breach-banner
  channel is committed for v1.]`

## 7. Retention

- Email + auth metadata: while the account exists; immediate erasure via Delete my
  account.
- Crash reports: Sentry retention window then auto-deleted. `[UNVERIFIED — confirm
  exact retention days on the Sentry plan; prior docs claim 90 days.]`
- Roster/logbook data: on the device until the user deletes it.

## 8. Children

Not intended for users under **16**, and not directed at children. We do not
knowingly collect data from anyone under 16. *Evidence*: eligibility 16+ in
`docs/store/terms-of-service.md` §3. The store **content rating** is 4+ / Everyone
(no objectionable content), while the **minimum age of use** is 16 and the Play
**target audience** is adults — these are distinct axes and are intentionally set
this way (Gerardo decision 2026-07-11, resolves store-prep-report D-2).

## 9. Changes

Material changes bump the "Last updated" date + notify in-app/email; a new
processing purpose requires fresh opt-in consent.

## 10. Contact

`devsupport@lizentics.com` (subject line: "Privacy").
Lizentics Talent FZE, Ajman, United Arab Emirates.
