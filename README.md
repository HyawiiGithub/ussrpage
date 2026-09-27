# UNION OF SOVIET SOCIALIST REPUBLICS — ussrpage

Official server record: **Leadership • Structure • History • Join**.
Gosplan brutalist UI (flat crimson `#8a0f14`, paper `#e8dcc6`,
`IBM Plex Mono` + `Playfair Display`).

- Invite: https://discord.gg/soviets
- Other-site button migrates to the other site (link in Settings).

## How saving works (read this once)

`data.json` in this repo **is** the site. Every visitor loads exactly that
file — so whatever is committed here is what everyone sees. No database,
no rules, no console, nothing to break.

The committee menu (red dot, bottom-right, access code required) publishes
through the GitHub API: each save commits `data.json` with a message like
`almanac: update leadership`. Pages rebuilds in about a minute.

## Publishing setup (one time)

Saves need a token (kept in your browser tab only — never written anywhere):

1. GitHub → Settings → Developer settings → Personal access tokens →
   **Tokens (classic)** → Generate new.
2. Tick the **`repo`** scope, generate, copy the `ghp_…` value.
3. Open the site → committee menu → unlock → **Publish tab** → paste →
   remember. Done for that tab.
4. Delete the token on GitHub any time to revoke.

Without a token, edits are kept on your device (local draft) and the menu
says so — nothing silently pretends to save.

## Editing

- **Pages tab** — History and any pages you create render from text.
  Overview, Leadership and **Structure are automatic** (Structure is built
  live from your categories + roll — High Command first, then the rest).
  Pages marked ★ cannot be deleted.
- **Leadership tab** — add / remove leaders, change name, post, Russian
  title, rank, bio, category, status (**LEADER** = currently leading, red
  stamp; **OFFICIAL** = in office; **VETERAN** = former/honorary), reorder
  with ↑↓. Photo per leader: paste an image link, or pick a file (GIFs keep
  moving up to 3 MB, stills are shrunk in-browser).
- **Categories box** — sections on the Leadership page, top to bottom.
  Removing one moves its leaders to Leadership.
- **Settings tab** — motto, ticker line, invite, other-site button link+label.

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
