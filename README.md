# USSR CENTRAL ALMANAC — ussrpage

Official server record: **Leadership • Structure • History • Join**.
Gosplan brutalist UI (flat crimson `#8a0f14`, paper `#e8dcc6`,
`IBM Plex Mono` + `Playfair Display`).

- Invite: https://discord.gg/soviets
- Other-site button migrates to the other site (link in Settings).
- No numbers content lives here by design — one button only.

## Files (static — GitHub Pages, root)

- `index.html` — whole site + committee menu (Firebase via CDN, no build)
- `data.json` — fallback seed (used only if the database is unreachable)
- `updates.json` — REMOVED (no decrees feed in this design)

## Editing (no code needed)

Open the site → red dot (bottom-right) or committee button → enter the
**access code** (sent privately to the owner — never stored in this repo,
only its salted SHA-256 hash is in `index.html`).

- **Pages tab** — edit Structure / History / Join text, or create new pages
  (they appear in the top menu automatically). Overview and Leadership and
  Join shells cannot be deleted.
- **Leadership tab** — add / remove leaders, change name, post, Russian
  title, rank, bio, status (**LEADER** = currently leading, red stamp;
  **OFFICIAL** = in office; **VETERAN** = former/honorary), reorder with ↑↓.
  Photo per leader: paste an image link, or pick a file (shrunk + stored automatically).
- **Settings tab** — motto, ticker line, invite, other-site button link+label.

Everything saves to Firebase and appears for everyone instantly.

## Firebase setup (one time, ~1 min)

Content lives in the `union-of-gaming-court` project's **Realtime Database**
(config is already in `index.html` — the apiKey is public by design).
Photos need no bucket: picked files are shrunk in the browser and stored
as text alongside the record.

1. **Realtime Database** → Create database → region `europe-west1` → start
   in **locked mode**, then replace Rules with:
   ```json
   {
     "rules": {
       "ussrpage": {
         ".read": true,
         ".write": true
       }
     }
   }
   ```
   Publish. (Write is open so the committee menu can save without logins;
   the access code gates the UI. Tighten later with Auth if you want.)
   Until this is done, the menu keeps your edits on your device and says
   DATABASE LOCKED instead of crashing.
2. Open the live site once, unlock with the code, press **save leadership**
   once — this seeds `ussrpage/v1` in the database. Done.

## Deploy

```bash
git add index.html data.json README.md
git commit -m "feat: almanac v2 — firebase committee menu, invite + other-site button"
git push -u origin main
```

Pages: repo **Settings → Pages → Deploy from branch → main / root**.
Site: `https://hyawiigithub.github.io/ussrpage/`

## Changing the access code

Generate a new code, take its SHA-256 hex of `USSR-ALMANAC::v1` + code
(e.g. `python3 -c "import hashlib;print(hashlib.sha256(('USSR-ALMANAC::v1'+'YOUR-CODE').encode()).hexdigest())"`),
replace `CODE_HASH` in `index.html`, commit. The plaintext code must never
be committed — send it privately.
