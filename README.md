# UNION OF SOVIET SOCIALIST REPUBLICS — ussrpage

Official server record: **Leadership • Structure • History • Join**.
Gosplan brutalist UI (flat crimson `#8a0f14`, paper `#e8dcc6`,
`IBM Plex Mono` + `Playfair Display`).

- Invite: https://discord.gg/soviets
- Other-site button migrates to the other site (link in Settings).

## The wiki (read this once)

This is a wiki. Anyone holding the **access code** can modify EVERYTHING —
no tokens, no console, no rebuilds:

- Every view has **Read / Edit / History** tabs (Leadership has Read /
  Edit roll / History; Structure is built live from the roll).
- **Edit tab:** toolbar (bold, italic, heading, list, link, photo), live
  preview, and a summary line. If someone saved while you were writing,
  you get an edit-conflict warning before anything is overwritten.
- **History tab:** every version with author + summary. View any old
  version, revert with one click (roll reverts carry photos over).
- **Changes** in the top menu: the whole Union's recent edits, newest
  first, each linking straight to its version.
- Every edit is signed with the name you enter under the code box.

Saves write to the Union database (Firebase) and appear for everyone
instantly. `data.json` in this repo is only the fallback seed for visitors
whose network blocks the database.

## Editing guide

- **Pages tab (menu)** — raw store for History and custom pages, with
  summaries. Overview, Leadership and Structure are automatic ★.
- **Leadership tab (menu)** — add / remove leaders, change name, post,
  Russian title, rank, bio, category, status (**LEADER** = currently
  leading, red stamp; **OFFICIAL** = in office; **VETERAN** =
  former/honorary), reorder with ↑↓. Photo per leader: paste a link or pick
  a file (GIFs keep moving up to 3 MB, stills are shrunk in-browser).
- **Categories box** — sections on the Leadership page, top to bottom.
  Removing one moves its leaders to Leadership.
- **Settings tab** — motto, ticker line, invite, other-site button link+label.

## Firebase setup (one time, ~1 min)

Content lives in the `union-of-gaming-court` project (config is already in
`index.html` — the apiKey is public by design). History lives there too,
under the same node — nothing extra to create.

1. **Realtime Database** → Create database → region `europe-west1` →
   start in **locked mode**, then replace Rules with:
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
   Publish. (Write is open so the code-holders can save without logins;
   the access code gates the UI. Tighten later with Auth if you want.)
   Until this is done, saves fail loudly in the menu instead of silently —
   nothing pretends to save.
2. Open the live site once, unlock, save anything once — this seeds
   `ussrpage/v1` (content + empty history). Done.

## Deploy / manual edits

```bash
git add index.html data.json README.md
git commit -m "feat: ..."
git push -u origin main
```

Pages: repo **Settings → Pages → Deploy from branch → main / root**.
Site: `https://hyawiigithub.github.io/ussrpage/`

## Changing the access code

Generate a new code, take its SHA-256 hex of `USSR-ALMANAC::v1` + code
(e.g. `python3 -c "import hashlib;print(hashlib.sha256(('USSR-ALMANAC::v1'+'YOUR-CODE').encode()).hexdigest())"`),
replace `CODE_HASH` in `index.html`, commit. The plaintext code must never
be committed — send it privately.
