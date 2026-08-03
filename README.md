# Custom Homepage

**English** · [한국어](README.ko.md)

A single-file, offline-first homepage for your browser — no server, no build step, no dependencies. Open `index.html` locally and set it as your Safari (or Chrome) new-tab/homepage page.

Styled after Anthropic's Claude look: ivory/charcoal backgrounds, a coral accent, and a serif display face.

<img width="1710" height="944" alt="image" src="https://github.com/user-attachments/assets/c4b95ff0-392c-4bdc-8bcc-8e64cd427b97" />


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
- **Sync across devices** — optionally keep your shortcuts, to-dos, and theme in sync between machines using a private GitHub Gist (see [Sync across devices](#sync-across-devices) below).
- **Mobile-friendly** — responsive layout that adapts to phone screens (corner buttons fold into a top row, larger tap targets, no iOS zoom-on-focus).

Everything you customize (shortcuts, to-dos, theme, history) is saved in your browser's `localStorage`. Nothing leaves your machine unless you deliberately turn on Sync, which stores data in a **private** Gist under your own GitHub account.

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
   Chrome has three separate "start page" concepts, and each needs its own setting:

   **A. Home button page** (the page the 🏠 home icon takes you to)
   1. Go to `chrome://settings/appearance` (or **⋮ menu → Settings → Appearance**).
   2. Turn on **Show home button**.
   3. Choose **Enter custom web address**, and paste the full `file:///...` path from step 2 above.
   4. If the home button isn't visible in your toolbar, it's this same toggle — turning it on makes the icon appear next to the address bar.

   **B. Startup page(s)** (what opens when Chrome launches)
   1. Go to `chrome://settings/onStartup` (or **⋮ menu → Settings → On startup**).
   2. Select **Open a specific page or set of pages**.
   3. Click **Add a new page**, paste the same `file:///...` path, and click **Add**.

   **C. New-tab page** (what shows when you open a new tab / press ⌘T)
   Chrome does not let a local file replace the built-in New Tab page directly — this always needs a small extension:
   1. Install **[New Tab Redirect](https://chromewebstore.google.com/detail/new-tab-redirect/icpgjfneehieebagbmdbhnlpiopdcmna)** from the Chrome Web Store.
   2. Go to `chrome://extensions`, find **New Tab Redirect**, click **Details**, and enable **Allow access to file URLs** (required — without this the extension can't open a `file://` page).
   3. Click the extension's **Options** (or right-click its toolbar icon → **Options**).
   4. Under **Redirect URL**, paste the same `file:///...` path, then save.
   5. Open a new tab to confirm it loads the homepage.

   You don't need to set up all three — pick whichever entry points you actually use (most people just want B and/or C).

4. Open a new window/tab and you should see your new homepage. Click the **+** tile to start adding your own shortcuts.

## Sync across devices

By default your data is stored in `localStorage`, which is scoped **per browser and per machine** — a `file://` copy, a hosted `https://` copy, and a second laptop are all separate stores and won't share anything. The optional **Sync** feature bridges them by saving your shortcuts, to-dos, and theme to a single **private GitHub Gist** that every device reads from and writes to.

> History is intentionally **not** synced, to keep your browsing log private to each device.

### 1. Create a GitHub token (once)

1. Go to **[github.com/settings/tokens/new](https://github.com/settings/tokens/new?scopes=gist&description=Homepage%20sync)** (Personal access tokens → **Tokens (classic)**).
   - It must be a **classic** token — fine-grained tokens do **not** work with the Gist API.
2. Give it a name (e.g. `Homepage sync`) and check **only** the **`gist`** scope. Nothing else.
3. Generate the token and copy it (it looks like `ghp_...`).

### 2. Set up your first device

1. Click the **Sync** button (the circular-arrows icon, top-right corner).
2. Paste your token into **GitHub token**.
3. Leave **Gist ID** empty (this is the first time).
4. Click **Push**. This creates a new private Gist and auto-fills the **Gist ID** field — **copy that Gist ID**, you'll need it on the other device.

### 3. Set up your other devices

1. Open the same homepage on the second device and click **Sync**.
2. Paste the **same token** and the **Gist ID** you copied from the first device.
3. Click **Pull** to bring down your shortcuts, to-dos, and theme.

That's it. From now on:

- **Auto-push** — after you change a shortcut, to-do, or the theme, the page automatically pushes to the Gist (2-second debounce). No need to open the dialog.
- **Auto-pull** — each time the page loads, it silently pulls the latest data from the Gist, so a device picks up changes made elsewhere.
- **Manual Push / Pull** — always available from the Sync dialog if you want to force it.

The token and Gist ID are stored only in that browser's `localStorage` (`hp.sync.token`, `hp.sync.gistId`).

### ⚠️ Security note

**Only ever paste your token into the Sync dialog's token field** — never into a shortcut name/URL or a to-do. Those fields are synced into the Gist's contents, and GitHub's secret scanning will detect the token there and **automatically revoke it** (even in a private Gist). If that happens, generate a new token and Push again.

### Resetting sync on a device

If a device gets stuck with a stale Gist ID, open the browser's developer console on the page and run:

```js
localStorage.removeItem('hp.sync.gistId');
localStorage.removeItem('hp.sync.token');
location.reload();
```

Then re-enter the correct token and Gist ID in the Sync dialog.

## Notes & limitations

- This is designed to be opened as a local `file://` page — no server required, and it will keep working offline (shortcuts, to-dos, and history all still work; only favicon images and search suggestions need an internet connection).
- Favicons are fetched from Google's public favicon service. If a site has no cached icon, or you're offline, the shortcut falls back to a colored initial tile automatically.
- Browsers do not allow web pages to read your browser's real history — the **History** page here only logs things you click *from this homepage itself* (shortcuts, Google apps, AI links, or a typed address), capped at the last 50 entries.
- Optimized for Safari on macOS, but works in other modern desktop browsers and on mobile (the layout is responsive).
- All data lives in `localStorage`, scoped per-browser and per-machine, so it won't sync across devices or browsers on its own — turn on [Sync](#sync-across-devices) if you want your shortcuts and to-dos shared between machines.

## License

Feel free to fork and customize for your own homepage.
