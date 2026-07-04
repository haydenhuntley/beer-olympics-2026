# Security notes — Firebase keys & hardening

## TL;DR: the config keys are NOT secrets
The values in `firebase-config.js` (`apiKey`, `authDomain`, etc.) are **public by
design**. A Firebase *web* config only identifies the project — it grants no access by
itself. Any client-side app ships these to the browser, so on a static site (GitHub
Pages) they **cannot be hidden**, and hiding them would give zero real security.
Google documents this explicitly. So: leave them in the file; don't gitignore or
obfuscate them.

Real security = **database rules** + **API-key restrictions**, below.

## Step 1 — Lock the database (rules) ✅ prepared, needs deploy
`database.rules.json` is committed and ready. It changes the database from wide-open
test mode (`.read/.write: true` at the root) to: **everything denied except the app's
own `tournament2026` path.** This limits blast radius while keeping live sync working.

Deploy it (you're already logged in via the Firebase CLI):

```bash
npx -y firebase-tools deploy --only database
```

(`firebase.json` and `.firebaserc` are committed so this is a one-liner.)

> Was NOT auto-applied because cloud-mutation calls were permission-gated in the
> automated environment. The rules file itself is safe — the app only ever reads/writes
> `tournament2026`, so confining access to that path won't break anything.

## Step 2 — Restrict the public API key by HTTP referrer (recommended)
So the exposed key is useless if copied onto someone else's site:

1. Open **https://console.cloud.google.com/apis/credentials?project=beer-olympics-2026-22ac7**
2. Under **API Keys**, click the browser key (`AIzaSy…xLM4`).
3. **Application restrictions → HTTP referrers**, add:
   - `https://haydenhuntley.github.io/*`
   - `http://localhost:*` (for local testing)
4. Save. (Propagation can take a few minutes.)

This is safe for this app because it uses Realtime Database (governed by rules, not the
API key) and no Firebase Auth, so the referrer restriction won't break sync.

## Note on test mode expiry
The database currently allows public read/write so relatives can log scores with no
login — intended for the event. If you keep the project long-term, deploy Step 1 and
consider adding data-shape validation or requiring sign-in after the tournament.
