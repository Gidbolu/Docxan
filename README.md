# Docxan

**Offline-first Android app for scanning, organizing, and backing up documents.**

## Project Structure

- `app/` — Flutter application (`applicationId`: `app.docxan`, `minSdk`: 26)
- `supabase/` — Authentication, PostgreSQL (metadata), and Edge Function for generating R2 presigned URLs
- `legal/` — Privacy Policy and Terms of Service (Google Play)
- `tool/` — Cloudflare R2 smoke test
- `packages/` — Empty in the MVP; modules will be extracted later

**Architecture Rules:**

- Features must not import other features directly.
- Shared functionality belongs in `app/lib/core`.
- `app/lib/app` serves as the composition root.

## Local Setup

Run the development version:

```bash
cd app
flutter pub get
flutter run --flavor dev -t lib/main_dev.dart
```

Run the production version:

```bash
flutter run --flavor prod -t lib/main_prod.dart
```

## Required Accounts (Day 1)

1. **Google Play Console**
2. **Supabase** — Setup guide: [docs/supabase.md](docs/supabase.md)
3. **Cloudflare R2** — Buckets `doxan-backups-dev` and `doxan-backups-prod` (completed)
4. **Google Cloud OAuth** — Debug SHA-1 and Google Play App Signing configuration

Copy `app/env.example.json` to `app/env.json`.

**Note:** `env.json` is excluded from version control and must not be committed to the repository.

### Running with Supabase

Once Supabase is configured:

```bash
cd app
flutter run --flavor dev -t lib/main_dev.dart --dart-define-from-file=env.json
```

## Tech Stack

- **Flutter** — Cross-platform application framework
- **Riverpod** — State management
- **go_router** — Navigation and routing
- **Drift** — Local database and offline-first data persistence
- **ML Kit OCR** — Optical Character Recognition
- **AES-256-GCM** — Document encryption
- **Supabase** — Authentication and PostgreSQL database
- **Cloudflare R2** — Cloud storage for document backups
