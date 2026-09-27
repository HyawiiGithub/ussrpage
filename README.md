# USSR CENTRAL ALMANAC — ussrpage

Official server record: **Leaders • Situation • 15 SSRs • Government • Decrees • Join**.
Same Gosplan brutalist UI as **USSR-stock** (flat crimson `#8a0f14`, paper `#e8dcc6`,
`IBM Plex Mono` + `Playfair Display`, 3px borders, stamp №).

Live numbers (GSI, inflation, gold, companies) stay on the sister site:
- Economy: https://ussr-stock.vercel.app
- Economy repo: https://github.com/HyawiiGithub/USSR-stock
- This almanac repo: https://github.com/HyawiiGithub/ussrpage

## Files (all static — GitHub Pages ready)

- `index.html` — whole site, 6 views (Overview / Leaders / SSRs / Government / Decrees / Join)
- `data.json` — EDIT THIS for leaders, situation, ministries, laws, join steps
- `updates.json` — EDIT THIS to publish decrees (newest first is auto-sorted)

## Publish an update (30 seconds)

1. Open `updates.json` on GitHub → pencil icon → add entry at the top:
```json
{
  "date": "2026-09-28",
  "tag": "DECREE",
  "title": "YOUR TITLE HERE",
  "body": "What changed, who signed, what citizens must do."
}
```
Tags used so far: `DECREE`, `ELECTIONS`, `ECONOMY`, `PLAN`, `WAR`, `KGB`, `ANNOUNCEMENT`.
2. Commit → Pages rebuilds (~1 min) → appears in Decrees view + PRAVDA ticker.

## Change a leader / the situation

Edit `data.json`:
- `leadership[]` → `name`, `desc`, `status` (ACTIVE / VACANT?), optional `img` URL
- `situation.headline / summary / status_lines[]`
- `meta.last_updated` → today's date (shown in header + stamp)

Commit → live.

## First-time deploy (replace blank page)

The repo currently holds a blank template `index.html`. Replace it:

```bash
git clone https://github.com/HyawiiGithub/ussrpage.git
cp index.html data.json updates.json ussrpage/
cd ussrpage
git add index.html data.json updates.json
git commit -m "feat: USSR Central Almanac — Gosplan UI, leaders, SSRs, decrees feed"
git push -u origin main
```

Then enable Pages: repo **Settings → Pages → Deploy from branch → main / root**.
Site: `https://hyawiigithub.github.io/ussrpage/`

## Design lock (matches USSR-stock)

- No gradients / no glow. Flat fills only.
- Borders `#111`, hard shadows `3-4px`, stamp rotated `-1deg`.
- If you restyle, keep `:root` tokens identical to USSR-stock `index.html` so the two sites read as one system.
