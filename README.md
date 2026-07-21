# Custom Homepage

A single-file, offline-first homepage for your browser — no server, no build step, no dependencies. Open `index.html` locally and set it as your Safari (or Chrome) new-tab/homepage page.

Styled after Anthropic's Claude look: ivory/charcoal backgrounds, a coral accent, and a serif display face.

![screenshot placeholder](#)

## Features

- **Shortcuts grid** — one-click tiles to your favorite sites, with real site favicons (falls back to a colored initial tile if no icon is available).
  - Click **Edit** to enter edit mode: drag tiles to reorder, click a tile to edit its name/address, or hit the **×** to delete it.
  - Click the dashed **+** tile to add a new shortcut.
- **Search bar** — auto-focused on page load. Type a search term to search Google, or type a URL/domain to go straight there. Live autocomplete suggestions appear as you type (via Google Suggest).
- **History page** (`history.html`) — a simple log of shortcut clicks and direct addresses you've navigated to from this page (plain search queries are **not** logged, for privacy). Click any entry to revisit it, or clear the whole log with one button.
- **To-dos** — a lightweight checklist. Add tasks, check them off, clear completed ones. Saved locally.
- **Clock, date, and greeting** — updates live, with a greeting that changes based on time of day.
- **Dark / light mode** — follows your system setting by default, or toggle manually with the corner button (persists your choice).
- **Google apps menu** — click the dotted icon (top right) for quick links to Gmail, Drive, Calendar, Docs, YouTube, and more, with official Google icons.
- **AI shortcuts** — Gemini / ChatGPT / Claude icons pinned to the top left.

Everything you customize (shortcuts, to-dos, theme, history) is saved in your browser's `localStorage` — nothing is sent to any server.

## Getting started

1. **Download this repo** (or just the `index.html` and `history.html` files — they need to sit in the same folder).

   ```bash
   git clone https://github.com/<your-username>/custom_homepage.git
   ```

2. **Note the full local path** to `index.html`. For example:

   ```
   /Users/yourname/Documents/GitHub/custom_homepage/index.html
   ```

3. **Set it as your browser homepage.**

   ### Safari (macOS)
   - Safari menu → **Settings** → **General**
   - Set **Homepage** to the full file path in `file://` form, e.g.:
     ```
     file:///Users/yourname/Documents/GitHub/custom_homepage/index.html
     ```
   - Set **"New windows open with"** (and/or **"New tabs open with"**) to **Homepage**.

   ### Chrome
   - Chrome menu → **Settings** → **On startup** → **Open a specific page** → add the same `file:///...` path.
   - For the **new-tab page** specifically, Chrome doesn't allow a local file to replace it directly — you'd need an extension (e.g. "New Tab Redirect") pointed at the same `file://` path.

4. Open a new window/tab and you should see your new homepage. Click the **+** tile to start adding your own shortcuts.

## Notes & limitations

- This is designed to be opened as a local `file://` page — no server required, and it will keep working offline (shortcuts, to-dos, and history all still work; only favicon images and search suggestions need an internet connection).
- Favicons are fetched from Google's public favicon service. If a site has no cached icon, or you're offline, the shortcut falls back to a colored initial tile automatically.
- Browsers do not allow web pages to read your browser's real history — the **History** page here only logs things you click *from this homepage itself* (shortcuts, Google apps, AI links, or a typed address), capped at the last 50 entries.
- Desktop browsers only for now; no mobile-specific layout.
- All data lives in `localStorage`, scoped per-browser and per-machine — it won't sync across devices or browsers.

## License

Feel free to fork and customize for your own homepage.
