# CookUnity On-Hold Ticket Tracker (GitHub Pages + Apps Script)

A dashboard for tracking on-hold Zendesk tickets. The frontend is hosted on **GitHub Pages** and calls a **Google Apps Script** backend that reads/writes a **Google Sheet** as the database.

## Architecture

```
┌──────────────────────────────────┐
│  User's browser                  │
│  → cookunity-onhold.github.io    │  (GitHub Pages hosts index.html)
└───────────────┬──────────────────┘
                │  Google Sign-In (only @cookunity.com allowed)
                │  fetch() calls with ID token
                ↓
┌──────────────────────────────────┐
│  Google Apps Script Web App      │  (verifies ID token,
│  → JSON API                       │   restricts to @cookunity.com)
└───────────────┬──────────────────┘
                ↓
┌──────────────────────────────────┐
│  Google Sheet "OnHold Tracker DB"│
└──────────────────────────────────┘
```

## Deployment steps

Follow **DEPLOY.md** — it walks through each step with screenshots.

## Files

- `src/index.html` — the whole frontend (GitHub Pages serves this)
- `src/Code.gs` — the backend API (paste into Apps Script editor)
- `src/appsscript.json` — Apps Script manifest

## Configuration

Before deploying, edit **two lines** in `src/index.html`:

```javascript
const GOOGLE_CLIENT_ID = '311124993732-...apps.googleusercontent.com';  // ← already filled in
const APPS_SCRIPT_URL  = 'REPLACE_WITH_YOUR_APPS_SCRIPT_WEB_APP_URL';    // ← paste after deploy
```

And **one line** in `src/Code.gs`:

```javascript
const ADMIN_EMAILS = [
  'your.email@cookunity.com',   // ← put your email here
];
```
