# Fortt Media · Bible Tools

A suite of free, mobile-first web tools for reading, studying, and exploring Scripture. All tools run as static sites on GitHub Pages — no server, no framework, no build step. Custom domain: `a.fortt.com`.

---

## Projects

### Today's Bible Character (`/web/today.html`)

A daily devotional app that assigns one unique person from Scripture to each day of the year, guided by the liturgical calendar. Users see a first-person "Who am I?" riddle, guess the character, then tap to reveal their identity with biographical details and a link to the Study Bible.

- **406 characters** mapped to liturgical positions via anchor-relative offsets
- **Year-aware:** computes Easter dynamically, adapts season boundaries for any year
- **Two-screen scroll-snap layout:** context screen (brand, season, date, "why today") + riddle screen (hint, reveal, navigation)
- **Subscription gate:** first-day free, then requires email via Kit form
- **PWA installable** with dark theme, oil lamp icon

**Repo:** `web` · **Entry point:** `today.html`

---

### Study Bible (`/web/`)

A full-featured Bible reading app serving the public-domain World English Bible (WEB) with integrated reference tools.

- **31,102 verses** across 66 books, fetched from a static JSON API
- **2,708 glossary terms** (people, places, doctrine, terms, groups) via sql.js (WASM) — queried client-side, no server
- **14,089 verses with glossary pills** via whole-Bible per-verse text matching
- **590 major passage markers** with green sidebar bars and Matthew Henry's Commentary
- **Word-level lookup:** tap any word for glossary matches, Strong's Hebrew/Greek numbers, Webster's 1913 definitions
- **Alias search:** "Cephas" finds "Peter", "Horeb" finds "Mount Sinai"
- **Deep linking:** `#Book/Chapter/Verse` URLs for any passage
- **PWA installable** with offline support

**Repo:** `web` · **Entry point:** `index.html`

---

### Bible Glossary (`/glossary-app/`)

A standalone browser for the Bible glossary database — the same 2,708-term dataset that powers the Study Bible, presented as a searchable, browsable reference.

- **Sections:** Books (66), OT People (1,065), NT People (232), Places (308), Groups (104), Doctrine (337), Terms (596)
- **Cross-references and relationships:** 22,116 relationship rows, 8,612 cross-refs
- **Quality-audited** through four scholarly personas (historical-critical, Jewish studies, systematic theology, pastoral)
- **Dark/light theme** with the shared Cormorant Garamond + DM Sans typography system

**Repo:** `glossary-app` · **Entry point:** `index.html`

---

### Bible Names (`/bible-names/`)

A name discovery tool for exploring the meanings, origins, and stories behind 1,200+ biblical names.

- **Browse by popularity** with a rarity slider (common ↔ rare)
- **Search and filter** by name, gender, and testament
- **Detail cards** with etymology, original word, first appearance, family connections, and books
- **Share cards:** generate and save name cards as images

**Repo:** `bible-names` · **Entry point:** `index.html`

---

### Subscribe (`/web/subscribe.html`)

Email subscription landing page for Fortt Media Bible Tools updates. Uses Kit (ConvertKit) inline form styled to match the dark/gold design system.

**Repo:** `web` · **Entry point:** `subscribe.html`

---

## Architecture

All projects share:

- **Single-file apps:** each is one HTML file with embedded CSS, JS, and (where needed) data
- **No server:** everything runs client-side, served from GitHub Pages
- **No framework:** vanilla HTML/CSS/JS throughout
- **Shared design system:** dark background (`#0C0F14`), gold accents (`#C9A84C`), cream text (`#F2E8D5`), Cormorant Garamond for display text, DM Sans for UI chrome
- **PWA support:** manifest, service worker, install banners, offline capability
- **Static data:** SQLite via sql.js WASM, JSON APIs, embedded JS constants — no backend

## Repositories

| Repo | Contains | GitHub Pages path |
|---|---|---|
| `ntvckmpm42-ui.github.io` | This landing page | `/` (root) |
| `web` | Study Bible, Today's Bible Character, Subscribe, liturgical data, glossary DB | `/web/` |
| `glossary-app` | Bible Glossary browser, source CSVs, build pipeline, audit scripts | `/glossary-app/` |
| `bible-names` | Bible Names discovery tool | `/bible-names/` |

## Custom Domain

`a.fortt.com` is configured via CNAME to `ntvckmpm42-ui.github.io`. All repos are accessible at `a.fortt.com/{repo-name}/`.

## Cross-App Navigation

All apps link to the Study Bible for verse references. Links include a `?from=` parameter that triggers a floating back button in the Study Bible:

| Source App | Parameter | Back Button |
|---|---|---|
| Today's Bible Character | `?from=today` | ← Back to Today's Bible Character |
| Bible Names | `?from=names` | ← Back to Bible Names |
| Bible Glossary | `?from=glossary` | ← Back to Bible Glossary |

This solves the iOS PWA limitation where standalone mode opens links in the same window with no browser back button. All external links use `window.open()` for new-tab behavior on desktop/Android browsers.

## PWA Support

All four apps are installable as PWAs with manifest, service worker, and install banners:

| App | Manifest | Service Worker | Cache |
|---|---|---|---|
| Study Bible | `manifest.json` | `sw.js` (v5) | Full app + DB |
| Today's Bible Character | `today-manifest.json` | `today-sw.js` (v3, scoped to today files) | App + icons |
| Bible Names | `names-manifest.json` | `names-sw.js` (v1) | App + icons |
| Bible Glossary | *(no PWA wrapper yet)* | — | — |

The Today's Bible Character service worker is scoped to only cache `today*` and `subscribe*` files, allowing Study Bible requests to pass through to the network or the Study Bible's own service worker.

---

## Credits

- World English Bible (WEB) — public domain
- Easton's Bible Dictionary (1897) — public domain
- STEPBible TIPNR dataset — CC BY 4.0 (Tyndale House Cambridge)
- Matthew Henry's Complete Commentary — public domain
- Webster's Unabridged Dictionary (1913) — public domain
- Original content — Fortt Media

---

## License

© 2026 Jon Fortt, Fortt Media. All rights reserved.

Designed and built by Jon Fortt, Fortt Media.
