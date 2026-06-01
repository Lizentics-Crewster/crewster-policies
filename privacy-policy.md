# Crewster Privacy Policy

**Last updated**: 2026-06-01
**App version**: v1.0
**Status**: Draft — in-repo until publication at Bloque E (public URL).

---

## Summary (TL;DR)

- **Your roster data NEVER leaves your device.** PDFs you import + the
  duties extracted from them stay in your phone's local storage.
  Crewster has no server-side roster database.
- **Account email** is the ONLY personal information we collect. It is
  stored in Supabase (EU region) to authenticate you across devices.
- **Anonymous crash reports** are sent to Sentry (EU region) to help
  us fix bugs. You can disable this in **Settings → Privacy → Crash
  reports**.
- **No advertising trackers, no analytics, no third-party SDKs other
  than the two named above.**
- **Encryption** — all network connections use HTTPS / TLS. Local
  data is protected by OS-level encryption (iOS Data Protection +
  Android file-based encryption), activated by your device
  passcode. Auth tokens live in iOS Keychain / Android Keystore.
  Full details in Section 6.

---

## 1. Who we are

Crewster is operated by **Lizentics** (Spain). Contact:
`crewster@lizentics.com`.

We are the **data controller** under the EU GDPR (Regulation (EU)
2016/679) and Spanish LOPDGDD (Ley Orgánica 3/2018) for the personal
data described below.

## 2. What data we collect

### 2.1 Email address (for authentication)

When you create an account, you supply an email + password. The email
is stored in our authentication provider, **Supabase** (operated by
Supabase Inc., processed in the **EU region** — Frankfurt).

We use the email solely to:

- Identify your account across reinstalls or new devices.
- Send password-reset OTP codes when you request them.
- Send the email verification link at sign-up.

**Legal basis (GDPR Art. 6(1)(b))**: necessary for the performance of
a contract (you cannot use the app without an authenticated account).

### 2.2 Roster data (LOCAL ONLY — never leaves your device)

When you import a PDF roster, Crewster:

- Saves the PDF to your phone's local app sandbox (`FileSystem`).
- Parses the PDF on-device using JavaScript regex.
- Stores the extracted activities + day summaries in a local SQLite
  database (WatermelonDB) on your phone.

**None of this data is uploaded anywhere.** There is no Crewster
server holding roster history.

### 2.3 Anonymous crash reports (opt-out)

When the app crashes or hits an unhandled error in production, a
crash report is sent to **Sentry** (operated by Functional Software
Inc., processed in the **EU region** — Frankfurt). Each report
contains:

- **Stack trace**: which file + line of code threw the error.
- **Breadcrumbs**: which screens you navigated to + which actions
  you tapped in the ~30 seconds before the crash.
- **Device info**: phone model, OS version, app version, available
  memory.
- **Pseudonymous user id**: your Supabase account UUID (e.g.
  `7f3a9b2c-...`), **NOT your email**. We use this to count "how
  many users hit this same bug?" — we cannot work backward from
  the UUID to your email.

**What is NEVER in a crash report**:

- Your email address (stripped at the boundary).
- Any roster data (PDFs, duties, flight numbers, airport codes you
  fly to, etc.).
- Any text you typed (we never capture form input).
- Any authentication token.

**Legal basis (GDPR Art. 6(1)(f))**: legitimate interest in
product stability. Balancing test passes because (a) data is
pseudonymous, (b) intrusion is minimal, (c) benefit (fewer crashes
for all users) is high, (d) you can opt out at any time in
**Settings → Privacy → Crash reports**.

If you opt out, crashes stop being sent immediately. We do not
retroactively delete prior crash reports — they remain in Sentry's
90-day retention window then are auto-deleted.

## 3. Who we share data with (sub-processors)

| Sub-processor                     | What they receive          | Where they process | Legal basis                        |
| --------------------------------- | -------------------------- | ------------------ | ---------------------------------- |
| Supabase Inc.                     | Your email + password hash | EU (Frankfurt)     | Art. 6(1)(b) — contract            |
| Functional Software Inc. (Sentry) | Anonymous crash reports    | EU (Frankfurt)     | Art. 6(1)(f) — legitimate interest |

Both sub-processors are bound by standard GDPR **Data Processing
Agreements (DPAs)** signed by Lizentics. No data is transferred
outside the European Economic Area.

## 4. We do NOT collect

To remove ambiguity:

- ❌ Advertising identifiers (no IDFA on iOS, no AAID on Android).
- ❌ Location (no GPS, no IP-derived geo).
- ❌ Camera / microphone / contacts / SMS.
- ❌ App usage analytics (no PostHog, no Mixpanel, no Google
  Analytics, no Firebase Analytics).
- ❌ Marketing / behavioral tracking of any kind.

## 5. Your rights (GDPR Articles 15-22)

You can exercise the following rights free of charge:

- **Right to access** (Art. 15): request a copy of the email + any
  associated metadata we hold.
- **Right to rectification** (Art. 16): change your email by
  contacting us.
- **Right to erasure** (Art. 17) "right to be forgotten": delete
  your account + the associated email from Supabase + all rosters
  on this device in one tap via **Settings → Privacy and Security
  → Delete my account**. The deletion is immediate + permanent
  (server-side erasure via a secure Edge Function, followed by
  local data cascade, followed by sign out). Roster data alone
  can also be wiped via **Settings → Delete all imported rosters**
  without deleting the account.
- **Right to data portability** (Art. 20): export your local
  roster data as JSON via **Settings → Privacy and Security →
  Export my data**. The exported file contains your profile,
  preferences, pay-rate settings, roster import history, and all
  parsed activities. PDF binaries are NOT included (they remain
  in your phone's email client where you originally received
  them).
- **Right to object** (Art. 21): opt out of crash reports via
  **Settings → Privacy → Crash reports**.

Contact `crewster@lizentics.com` to exercise any of these rights.
We respond within 30 days per GDPR Art. 12(3).

You also have the right to lodge a complaint with the Spanish
data protection authority (**AEPD**, https://www.aepd.es).

## 6. Security and encryption

### 6.1 In transit (network)

- **All connections to Supabase + Sentry use HTTPS / TLS 1.2+.**
  No plaintext credential or telemetry transmission. Certificate
  validation handled by the OS network stack on both iOS and
  Android.
- **No third-party servers receive your roster data.** Roster
  parsing happens entirely on your device; no network call
  carries roster bytes or duty data.

### 6.2 At rest (on your device)

- **Roster PDFs + parsed activities** live in your phone's local
  storage under the app's sandboxed data directory. On iOS, this
  directory is covered by **Apple's Data Protection**
  (`NSFileProtectionComplete`), which encrypts files at rest using
  a key derived from your device passcode. On Android, the same
  directory is covered by the OS's **file-based encryption (FBE)**,
  also activated by your device lock screen. **A device without a
  passcode / PIN / biometric / pattern lock is NOT encrypted at
  rest** — this is a platform limitation, not a Crewster choice.
- **Authentication tokens** (your Supabase session) are stored via
  `expo-secure-store`, which on iOS uses **Keychain Services** and
  on Android uses **Keystore**, both hardware-backed where
  available.
- **SQLite database** (`crewster.db` containing activities + roster
  metadata): currently encrypted only at the OS level (above).
  **Per-row / per-column encryption via SQLCipher is on the
  roadmap for v2.** v1 ships with OS-level encryption only because
  the SQLCipher integration would require a custom WatermelonDB
  adapter that the upstream library does not currently expose
  stably (see `CLAUDE.md` for the technical rationale).
- **Sentry crash reports** are encrypted in transit (TLS) and at
  rest by Sentry's EU-region infrastructure (SOC 2 Type II
  attested + EU Data Residency add-on per their DPA).

### 6.3 Your responsibility

- **Set a device passcode / PIN / biometric.** Without it, OS-level
  encryption is disabled and a stolen device exposes your roster
  data.
- **Keep your account password secure.** Crewster never asks for
  your password outside the sign-in / change-password flows. We
  will never email you asking for it.

### 6.4 Breach notification

If a security breach affecting your personal data occurs, we will
notify you within **72 hours** of becoming aware (per GDPR
Article 33) via in-app banner + email + the contact channels in
Section 10.

## 7. Data retention

- **Email + auth metadata**: kept while your account exists.
  Immediate erasure via in-app **Settings → Privacy and Security
  → Delete my account**. Email-based deletion requests
  (`crewster@lizentics.com`) processed within 30 days per GDPR
  Art 12(3).
- **Crash reports**: 90 days in Sentry then auto-deleted by their
  retention policy.
- **Roster data**: kept on your device until you delete it. We
  have no control over this — it lives in your phone's storage.

## 8. Children

Crewster is not intended for users under 16. We do not knowingly
collect data from anyone under 16. If you believe a child has
created an account, contact us and we will delete it.

## 9. Changes to this policy

When this policy materially changes, we will:

1. Update the "Last updated" date at the top.
2. Notify you via in-app banner or email.
3. Require re-consent if the change introduces a new processing
   purpose (e.g. if we ever add product analytics, that requires
   explicit opt-in, NOT legitimate interest).

## 10. Contact

For any privacy question, request, or complaint:

- **Email**: `crewster@lizentics.com`
- **Subject line**: please include "Privacy" so it routes correctly.
