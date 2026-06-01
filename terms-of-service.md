# Crewster Terms of Service

**Last updated**: 2026-06-01
**App version**: v1.0
**Status**: Draft — in-repo until publication at Bloque E (public URL).

---

## Summary (TL;DR)

- Crewster is a personal calendar tool for flight crews. It parses
  your roster PDFs **on your device**. We do NOT receive or store
  your roster data on our servers.
- We provide the app **AS IS**. Verify any duty information
  against your airline's official roster before flying — Crewster
  is NOT an FAA / EASA / OACI-compliant flight log.
- You must be **16 or older** + a commercial flight crew member.
- Lizentics operates the app from Spain. Spanish law + EU GDPR /
  LOPDGDD govern.

---

## 1. Acceptance of these terms

By creating an account, signing in, or otherwise using Crewster
(the "App"), you agree to these Terms of Service (the "Terms").
If you do not agree, do not use the App.

These Terms form a binding contract between you (the "User",
"you") and **Lizentics**, a Spanish entity operating from Spain
("Lizentics", "we", "us", "our"). Lizentics's contact channel for
all matters relating to these Terms is
`crewster@lizentics.com`.

You also agree to the [Privacy Policy](./privacy-policy.md),
which forms an integral part of these Terms.

## 2. The service

Crewster is a mobile application for iOS and Android that:

1. Receives PDF roster files shared from your phone (typically
   from your email client).
2. Parses those PDFs on your device using local JavaScript code.
3. Displays the extracted duties on an interactive monthly
   calendar.
4. Tracks changes when you re-import an updated roster of the
   same period.
5. (Optional, future) Estimates compensation based on pay-rate
   inputs you configure.

The App is designed for personal use by **commercial flight crew
members** (pilots, cabin crew, dispatchers, etc.). It is not
intended as a regulatory tool — see Section 6.

## 3. Eligibility

To use Crewster you must:

- Be **16 years of age or older**. Crewster is not directed at
  children, and we do not knowingly collect data from anyone
  under 16. See Privacy Policy Section 8.
- Be a current or former commercial flight crew member or
  authorised representative of one (e.g. crew scheduler).
- Be capable of forming a binding contract under the laws of
  your jurisdiction.
- Not be prohibited from using the App under applicable export
  controls, sanctions, or other laws.

If you are using Crewster on behalf of an organisation (e.g.
your airline's crew operations team), you represent that you
have authority to bind that organisation to these Terms.

## 4. Your account

To use the App you must create an account using a valid email
address + password. You are responsible for:

- Keeping your password secret. Crewster will never ask for it
  outside the sign-in / change-password flows.
- All activity occurring under your account.
- Notifying us at `crewster@lizentics.com` if you suspect
  unauthorised access.

You may close your account at any time via **Settings → Privacy
and Security → Delete my account**. Closure is **immediate +
permanent**: server-side erasure of your authentication record

- local cascade that wipes all roster data on your device + sign
  out.

## 5. Acceptable use

You agree to use Crewster only for lawful purposes related to
your own flight crew schedule (or a schedule you are authorised
to manage). You agree NOT to:

- Reverse engineer, decompile, or otherwise attempt to derive the
  source code of the App beyond what is permitted by Article 6 of
  Directive 2009/24/EC (interoperability exception).
- Use the App to violate any law, regulation, or airline
  operating procedure.
- Upload, parse, or otherwise process roster data belonging to
  other crew members WITHOUT their consent.
- Resell, sublicense, or commercially redistribute the App or
  its output.
- Use the App to circumvent your airline's official roster
  distribution channels.
- Attempt to access another user's account or data, or otherwise
  bypass authentication mechanisms.

We may suspend or terminate your account if we reasonably
believe you have violated this Section 5 or any other part of
these Terms. We will tell you why when we do so unless prevented
by law.

## 6. AS-IS disclaimer + accuracy warning

**CREWSTER PARSES YOUR ROSTER PDFs ON-DEVICE USING REGULAR
EXPRESSIONS.** Parsing accuracy depends on the airline's PDF
format remaining stable. Crewster:

- **Is not certified** by FAA, EASA, OACI, AESA, or any other
  aviation authority.
- **Is not a substitute** for your airline's official roster.
  Always verify duty times, flight numbers, departure / arrival
  airports, and crew assignments against the official roster
  before reporting for duty.
- **Is not a regulatory flight log.** Do NOT use Crewster to
  prove flight hours, training currency, FTL (Flight Time
  Limitations) compliance, medical reporting periods, or any
  other regulatory matter.
- **Cannot guarantee** parsing of every roster format, every
  PDF version, or every edge case. Bugs may cause duties to be
  missed, mis-typed, or misclassified.

The App is provided **"AS IS"** and **"AS AVAILABLE"** without
warranty of any kind, express or implied, including but not
limited to warranties of merchantability, fitness for a
particular purpose, accuracy, or non-infringement, **TO THE
MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW**. Some jurisdictions
do not allow exclusion of implied warranties; in those
jurisdictions our liability is limited to the minimum permitted
by law.

## 7. Your content

You retain ALL rights to the roster data you import into the
App ("Your Content"). Crewster does not claim any ownership.
Because your roster data stays on your device (see Privacy
Policy Section 2.2), we cannot access, modify, copy, or share
it.

You grant Crewster a limited, non-exclusive, revocable license
to read Your Content **on your device only** for the sole
purpose of parsing + displaying it in the App's calendar +
detail views. This license terminates immediately when you
uninstall the App or delete your account.

## 8. Intellectual property

The App, its source code (where not open-sourced), its UI
design, its iconography, the "Crewster" + "Lizentics" names +
logos, and the parsed-data display format are the intellectual
property of Lizentics, protected by Spanish + EU copyright,
trademark, and other applicable laws.

These Terms grant you a personal, non-exclusive, non-
transferable, revocable license to use the App on devices you
own or control. No other rights are granted.

Third-party libraries used by the App (React Native, Expo,
WatermelonDB, Supabase client, Sentry, lucide-react-native, etc.)
remain the property of their respective copyright holders and
are used under their respective open-source licenses, available
on request at `crewster@lizentics.com`.

## 9. Service availability

We aim to keep the App working but do not guarantee uptime or
availability of:

- Authentication (Supabase Auth EU region).
- Crash report upload (Sentry EU region — purely optional;
  opt-out via Settings → Privacy and Security → Crash reports).
- Future updates, bug fixes, or new airline parser support.

We may suspend the service for maintenance, security incidents,
or compliance with law. Roster data on your device remains
accessible regardless of service availability — it is parsed +
stored entirely locally.

## 10. Limitation of liability

To the maximum extent permitted by applicable law:

- Lizentics is **NOT liable** for any direct, indirect,
  incidental, consequential, special, or exemplary damages
  arising out of or related to your use of the App, including
  but not limited to:
  - Missed duties, delayed reports, fines, disciplinary
    actions, or contractual penalties imposed by your airline.
  - FTL violations, medical-currency lapses, or regulatory
    findings.
  - Lost data, lost income, or lost opportunities.
- Lizentics's total cumulative liability under these Terms is
  capped at **EUR 50** or the amount you have paid Lizentics in
  the 12 months preceding the claim, whichever is greater.
- Nothing in these Terms excludes or limits liability for:
  - Death or personal injury caused by Lizentics's negligence.
  - Fraud or fraudulent misrepresentation.
  - Any other liability that cannot be excluded by Spanish or
    EU law.

You acknowledge that you assume the operational risk of relying
on Crewster's parsed roster data and will independently verify
critical duty information against your airline's authoritative
source.

## 11. Indemnification

You agree to indemnify and hold harmless Lizentics, its
officers, employees, and contractors against any third-party
claims, damages, liabilities, costs, and expenses (including
reasonable legal fees) arising from:

- Your breach of these Terms.
- Your misuse of the App.
- Your processing of roster data belonging to another crew
  member without their consent.
- Your violation of any law or third-party right (including
  your airline's confidentiality obligations).

## 12. Termination

These Terms remain in effect until terminated by either party.

You may terminate at any time by deleting your account via
**Settings → Privacy and Security → Delete my account** or by
uninstalling the App.

We may terminate or suspend your account if you violate these
Terms, if we are required to do so by law, or if we discontinue
the App (with at least 30 days' notice where reasonably
possible).

Sections 6, 7, 8, 10, 11, 14, and 16 survive termination.

## 13. Changes to the App + Terms

We may update the App, add features, or change behavior at any
time. If a change materially affects your rights or obligations
under these Terms, we will:

1. Update the "Last updated" date at the top of these Terms.
2. Notify you in-app or by email.
3. Require re-acceptance if the change introduces a new
   processing purpose for your personal data (per Privacy
   Policy Section 9).

Continued use of the App after a non-material change
constitutes acceptance.

## 14. Governing law + jurisdiction

These Terms are governed by **Spanish law** + applicable
**European Union** law (in particular Regulation (EU) 2016/679
GDPR + Spanish LOPDGDD).

Any dispute arising out of or related to these Terms or the App
shall be resolved by the courts of **Madrid, Spain**, except
that:

- Consumers domiciled in another EU member state may bring a
  claim in the courts of their habitual residence per Regulation
  (EU) 1215/2012.
- Mandatory consumer-protection law in your jurisdiction may
  grant you additional rights.

For consumer disputes you may also use the European Commission's
**Online Dispute Resolution** platform at
https://ec.europa.eu/consumers/odr/ or contact us directly at
`crewster@lizentics.com` to attempt informal resolution.

## 15. Force majeure

Neither party is liable for failure or delay in performance
caused by circumstances beyond reasonable control, including
natural disasters, war, acts of terrorism, civil unrest,
governmental action, labour disputes, infrastructure outages,
or pandemic-related restrictions.

## 16. Miscellaneous

- **Entire agreement**: these Terms + the Privacy Policy
  constitute the entire agreement between you and Lizentics
  regarding the App.
- **Severability**: if any provision is held unenforceable, the
  remaining provisions remain in full force.
- **No waiver**: failure to enforce a provision does not waive
  the right to enforce it later.
- **Assignment**: you may not assign your rights under these
  Terms. Lizentics may assign its rights to a successor or
  affiliate.
- **Language**: these Terms are written in English. A Spanish
  translation may be provided for convenience; in case of
  conflict, the English version governs.
- **Notices**: notices to Lizentics must be sent to
  `crewster@lizentics.com`. Notices to you will be sent to the
  email associated with your account.

## 17. Contact

For any question, request, or complaint about these Terms:

- **Email**: `crewster@lizentics.com`
- **Subject line**: please include "Terms" so it routes
  correctly.
