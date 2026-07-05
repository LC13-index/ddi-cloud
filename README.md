# ddi-cloud

The remote content layer for the **Daily Design Inspiration** Chrome extension. Two JSON files, served free by GitHub Pages:

- **`highlights.json`** — articles pushed to every user's new tab (the accent strip). Polled hourly.
- **`catalog.json`** — the suggested-sources list and their categories. Polled every 6 hours. Edit it to fix a dead feed or add a source for all users without shipping an extension update.

## One-time setup

1. Upload these files to a **public** GitHub repo (e.g. `ddi-cloud`).
2. Repo **Settings → Pages** → Deploy from branch → `main` / root.
3. Verify `https://YOURUSERNAME.github.io/ddi-cloud/highlights.json` loads in a browser.
4. In the extension's `config.js`, set:
   - `CATALOG_URL:   "https://YOURUSERNAME.github.io/ddi-cloud/catalog.json"`
   - `HIGHLIGHTS_URL: "https://YOURUSERNAME.github.io/ddi-cloud/highlights.json"`
5. Reload the extension in `chrome://extensions`, open a new tab, hit Refresh.

⚠️ These URLs get baked into the shipped extension — treat them as permanent.

## Publishing a Highlight

Edit `highlights.json` (pencil icon on GitHub, or Pages CMS below), add an item at the top of `items`, commit. Fields:

| Field | Notes |
|---|---|
| `id` | Unique and stable — per-user dismissal keys off it. Never reuse. |
| `title`, `link` | Required. |
| `image` | Any hosted image URL (you can also upload to this repo's `/media` and use its Pages URL). |
| `source` | Label shown on the card. |
| `publishedAt` | ISO date. |
| `pinnedUntil` | ISO date — the highlight disappears for everyone after this. Omit to pin forever. |

## Editing with a UI instead of raw JSON

This repo includes a `.pages.yml` for [Pages CMS](https://pagescms.org) — a free, hosted, git-based CMS. Sign in with GitHub at pagescms.org, open this repo, and you get form-based editing for both files (add/remove/reorder highlights, date pickers, required-field validation). Every save is a commit. If a field type errors, check pagescms.org/docs for the current schema syntax.

## Graduation path

When you need drafts, scheduling, or multiple editors: Sanity or Payload (free tiers) publishing to this same JSON shape — the extension doesn't change.
