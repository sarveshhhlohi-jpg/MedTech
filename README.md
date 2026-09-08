# MEDIGUARD X

MEDIGUARD X is an AI Health + Insurance Safety OS prototype for structured patient intake, clinical safety review, and clinician-ready handoff.

It is built for a focused hackathon workflow: capture a patient's story, turn it into a structured record, surface allergy and medication risks deterministically, and produce a concise health timeline and doctor summary.

## Core Workflow

1. Sign in with Firebase Authentication.
2. Create a patient case using typed or voice-assisted intake.
3. Extract structured fields and review missing information or emergency signals.
4. Add document text for clinical field extraction.
5. Save the patient record to Firestore.
6. Review the allergy passport, medication safety workflow, timeline, and doctor summary.
7. Generate and share a PDF case sheet.

## Feature Status

| Capability | Status |
| --- | --- |
| AI-assisted case-taking | Complete |
| Patient health profile | Complete |
| Allergy profile and passport | Complete |
| Medication safety workflow | Complete |
| Document text extraction | Complete |
| Health timeline | Complete |
| Doctor-ready summary | Complete |
| PDF case sheet | Complete |
| Firebase patient persistence | Complete |
| Claim documentation readiness | Complete |
| Emergency safety card | Complete |
| Insurance policy analysis | Complete |
| Care finder and hospital matching | Complete as demo directory |
| Family mode caregiver handoff | Complete |

## Technology

- Flutter and Dart
- Firebase Authentication
- Email verification for newly registered accounts
- Cloud Firestore with authenticated per-user patient access rules
- Firebase App Check startup protection
- Speech-to-text intake
- PDF generation and sharing

## Setup

### Requirements

- Flutter SDK compatible with Dart 3.13 or later
- A configured Firebase project
- Android Studio or Xcode for mobile builds

### Run locally

```bash
flutter pub get
flutter analyze
flutter test
flutter run
```

Firebase configuration is generated in `lib/firebase_options.dart`, with Android configuration in `android/app/google-services.json`. For web release builds, provide `--dart-define=RECAPTCHA_V3_SITE_KEY=...` to activate App Check. Do not commit production credentials or broaden Firestore access rules for a deployed environment.

## Security Notes

- AI output is assistive extraction and summarization, not a diagnosis or autonomous clinical decision.
- Allergy and medication safety checks should remain deterministic and require clinician verification before real-world use.
- Firestore rules restrict patient records to the authenticated owner path: `users/{userId}/patients/{patientId}`.
- Firestore rules also whitelist the patient schema, enforce clinical field types and size limits, cap visit history at 100 entries, and restrict priority to `Routine`, `Review`, or `Urgent`.
- The prototype should use synthetic or consented demo data only.
- Before production, add App Check enforcement, audit logging, least-privilege roles, stronger schema validation, data retention controls, and a formal privacy/compliance review.
- Register Android, Apple, Windows debug tokens during local development, then enable App Check enforcement in the Firebase console only after release providers are verified.
- Configure Firebase email templates and require verified accounts before production access to clinical records.

## Validation

The automated suite covers AI extraction, profile and safety logic, document extraction, timeline and doctor summary behavior, claim documentation readiness, emergency safety card behavior, policy analysis, care matching, family handoff, and PDF generation.

```text
flutter test
17 tests passed
```

## Project Structure

```text
lib/
  app/                 App shell and theme
  features/
    auth/              Authentication and splash flow
    cases/             Intake and extraction workflow
    dashboard/         Patient overview and navigation
    records/           Patient record and clinical review views
  models/              Patient and visit models
  services/            AI, document, profile, safety, timeline, summary, claim, policy, care, family, and PDF services
test/                  Service and workflow regression tests
```
