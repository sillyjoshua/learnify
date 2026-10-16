# Learnify

Learnify is a free coding education desktop app with bite-sized lessons, accounts, saved progress, XP, leaderboards and a coding playground. No subscriptions, paid courses, streak pressure or paid XP boosts.

> **Early alpha:** this project is a source starter, not a finished production app. The desktop installer has not yet been built or tested. Python execution, email verification, password reset and production-grade isolated code execution are not implemented.

## Features

- Electron desktop shell for Windows, macOS and Linux
- Light responsive interface
- Account registration and sign-in with salted scrypt password hashes
- SQLite-backed sessions and progress
- Starter tracks for Python, JavaScript, and HTML/CSS
- XP awarded once per completed lesson after server-side answer verification
- Weekly and all-time leaderboards and public profiles
- JavaScript playground in a short-lived Web Worker
- No payments or streak tracking

## Run from source

Requirements: Node.js 20+ and npm. Internet is needed for the first dependency install.

```bash
npm install
npm run desktop
```

Build on the target operating system:

```bash
npm run desktop:win    # Windows NSIS installer
npm run desktop:linux  # Linux AppImage and .deb
npm run desktop:mac    # macOS .dmg
```

Build commands have not yet been run in this environment, so no tested installer is currently provided.

## Local server mode

```bash
npm install
cp .env.example .env
# Set SESSION_SECRET to a long random value before production use.
npm start
```

Open http://localhost:3000.

## Security notes

The Electron shell disables Node integration, enables context isolation and sandboxing, restricts navigation, and launches its API on loopback. The JavaScript Web Worker timeout prevents a common infinite-loop hang but is not a replacement for an isolated server-side sandbox. Never execute arbitrary user code on the application server. Before a broad public launch, add a dedicated isolated runner, email verification, password reset, account export/deletion, moderation, anti-cheat controls and observability.

For larger public deployments, migrate SQLite and its session store to managed PostgreSQL and a shared session store. Configure a strong `SESSION_SECRET` in production.

## Project layout

```text
public/  UI, styles and browser runner
src/     Electron main process, server and lesson catalogue
data/    SQLite database created at runtime (ignored by git)
```

## Licence

MIT. See [LICENSE](LICENSE).
