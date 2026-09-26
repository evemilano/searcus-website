# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **Searcus Swiss SAGL**, an SEO and Google Ads consulting agency based in Lugano, Switzerland. Founded 2010 by Giovanni Sacheli. Domain: searcus.ch

## Architecture

- **No build system** — plain HTML/CSS/JS served as static files. No bundler, no package manager, no compilation step.
- **Tailwind CSS via CDN** (`cdn.tailwindcss.com`) — utility classes applied directly in HTML. No local Tailwind config or build.
- **Custom CSS** in `assets/css/style.css` — full design system (~400 lines) built on CSS custom properties (dark palette: `--bg-void`, `--bg-obsidian`, `--bg-slate`; accent colors: signal, flare, ember, verified, cyan, violet). Includes: aurora mesh gradient animation (hero background), glassmorphism panels (`backdrop-filter`), smart navbar hide/show transition, card glow hover effects, dot grid pattern, typewriter animation (clip-path + steps), bidirectional marquee, scroll reveal with stagger delays + CSS `animation-timeline: view()` progressive enhancement, CTA button glow + ghost button styles, animated link underlines, terminal window chrome, JSON syntax highlighting, RSS ticker, segmented language toggle, `prefers-reduced-motion` safeguards, and `content-visibility: auto` for performance.
- **Custom cursor** in `assets/css/cursor.css` + three SVG files in `assets/images/cursor-{dot,caret,click}.svg` — **CSS-only, zero JS, zero rendering latency**. Uses native `cursor: url(...)` so the OS compositor draws the cursor, identical to the system pointer (no event/style/paint pipeline involved). Three states, each a 32×32 SVG with hotspot at 16,16: (1) **default** dot — 8×8 indigo block (`#6366F1`) with radial halo, applied to `html`; (2) **hover** caret — 2×20 cyan rectangle (`#06B6D4`), applied to `a, button, [role="button"], select, label, summary, [data-cursor]` (fallback `pointer`) and `input, textarea, [contenteditable="true"]` (fallback `text`); (3) **click** — 6×6 flare block (`#818CF8`), applied via `:active`. Native fallback `cursor: not-allowed` on disabled controls. Gated by `@media (hover: hover) and (pointer: fine)` so touch devices keep the native cursor unaltered. Trade-off vs the previous JS implementation: no animated blink on hover, no smooth color transition between states (the OS swaps cursor images instantly). Fully self-contained: delete the `<link>` to `cursor.css` from both `index.html` files to remove completely.
- **Chat terminal (RAG AI)** in `assets/css/chat-terminal.css` + `assets/js/chat-terminal.js` — plug-and-play AI chatbot that lives *inside* the hero `.terminal-window`. IIFE vanilla JS finds the terminal via CSS selector (no markup dependency), waits ~17.6s for the existing CSS typewriter animation to finish, then activates a welcome line and an input prompt `$ _` where the user can chat. New lines use `.terminal-static-line` (final typewriter state without `animation: typing` to avoid re-triggering the CSS keyframes). Bilingual strings detected from `document.documentElement.lang`. Session ID in `sessionStorage['searcus-chat-sid']`. Bot replies are animated char-by-char via `setTimeout` (disabled under `prefers-reduced-motion`). Responses include `[fonti]`/`[sources]` with clickable links restricted to a host whitelist (`www.evemilano.com`, `evemilano.com`) for XSS safety. All text goes through `escapeHtml()`; a minimal markdown renderer handles `**bold**`, `` `code` ``, and URLs. **Backend**: POSTs to `/api/chat` same-origin (see Production Hosting below). Fully self-contained: delete the two tags (`<link>` in head, `<script>` at end of body) from both `index.html` files to remove.
- **JS** in `assets/js/main.js` — six features (~170 lines): (1) mobile menu open/close with body scroll lock, (2) smart navbar that hides on scroll-down and reappears on scroll-up, (3) scroll-reveal via `IntersectionObserver` with fallback, (4) animated counters with cubic ease-out (supports `data-counter-dynamic` for computed values like years since founding), (5) dynamic copyright year, (6) RSS ticker fetching from `evemilano.com/feed/` with hardcoded fallback articles.

## Multilingual Setup

- Two languages: **Italian** (`/it/`) and **English** (`/en/`), each with its own `index.html`.
- `/` is 301-redirected to `/it/` by nginx (Italian is the default language); the root `index.html` is never served.
- Hreflang tags and `x-default` point to `/it/`.
- Language switcher links in the navbar point to the other locale's page.
- Content in each language file is fully duplicated (not templated) — **every change must be applied to both `/it/index.html` and `/en/index.html` simultaneously. The two pages must always stay in sync.** Never modify one without updating the other.

## SEO Assets

- `robots.txt` — allows all crawlers, references sitemap.
- `sitemap.xml` — lists both language versions with hreflang annotations. Must be updated when adding new pages. **After any HTML page modification, update the `<lastmod>` date in `sitemap.xml` for the affected URLs (format: `YYYY-MM-DD`).**
- Each page has Open Graph meta tags, canonical URLs, and hreflang links.

## Content Source: `backup/` Directory

The `backup/` directory contains markdown files with detailed content from the previous (more comprehensive) version of the site. These serve as the **authoritative source of truth** for company information, service descriptions, pricing, client lists, and copy. Key files:

- `company-info.md` — legal details, addresses, UID, team, pricing, client list
- `homepage.md` — full homepage content with navigation structure, services, and client list
- `seo-services.md` — detailed SEO consulting page content
- `google-ads.md` — Google Ads management page content
- `training.md` — course catalog, pricing, discount tiers, delivery formats
- `local-seo.md` — local SEO service page content
- `seo-manager.md` — SEO Manager service for enterprises
- `about-us.md` — company history and values

When creating or expanding pages, always reference these files for accurate copy, pricing, and service details rather than inventing content.

## Development

No build or install step. To preview locally, serve the directory with any static file server:

```
python3 -m http.server 8000
# or
npx serve .
```

## Production Hosting (nginx)

The site is served in production by nginx from this same directory (`root /home/giovanni/www/searcus.ch`). The vhost lives at `/etc/nginx/sites-available/searcus.ch`. Because the git repo, Claude config, and internal docs all live inside the document root, the vhost includes explicit rules that return `404` (not 403, so scrapers can't even confirm existence) for anything that isn't meant to be public:

- `location ~ /\.` — blocks any path containing a dotfile/dot-directory segment. Covers `.git/`, `.claude/`, `.env`, `.gitignore`, and any future hidden file.
- `location ~* ^/(CLAUDE\.md|tailwind\.config\.js)$` — blocks these two root-level project files (case-insensitive, anchored so it never matches files under `assets/`).
- `location ^~ /backup/` — blocks the entire `backup/` directory (internal markdown content, pricing, client list).

**When adding new non-public files to the repo root**, extend the relevant `location` block in the nginx vhost and reload with `sudo nginx -t && sudo systemctl reload nginx`. Anything publicly servable (new top-level HTML, new asset folder, etc.) does NOT need changes — the default `location /` with `try_files` still handles it.

### Redirect 301

All redirects live in the nginx vhost (none in the repo — the root `index.html` is never served):

- **HTTP → HTTPS** and **www → non-www**: port-80 server and a dedicated `server_name www.searcus.ch` 443 block both `return 301 https://searcus.ch$request_uri` (single hop).
- **`/` → `/it/`**: `location = /` in the main server.
- **Legacy URLs**: a `map $uri $searcus_redirect { ... }` table at the top of the vhost (regex, optional trailing slash), applied by a server-level `if ($searcus_redirect) { return 301 ...; }`. To add a redirect, add one line to the map and reload nginx.
- **410 Gone** for old WordPress leftovers: `location ~ /feed/?$` (all RSS feeds) and `location ^~ /wp-content/uploads/` (old media).

### `/api/chat` reverse proxy (chatbot backend)

The vhost also contains a `location = /api/chat` block that reverse-proxies POST requests to the `eve_rag` WordPress plugin running on the co-located `www.evemilano.com` site. The proxy uses loopback HTTPS (`proxy_pass https://127.0.0.1/wp-json/eve-rag/v1/chat`) with the `Host: www.evemilano.com` header rewritten and SNI set explicitly, so nginx on the evemilano vhost routes the call to WordPress with `REMOTE_ADDR = 127.0.0.1`. The plugin has a dedicated loopback-allowlist branch in `verify_chat_permission()` that authorizes this case without nonce or referer. Key safety settings inside the block:

- `limit_except POST { deny all; }` — only POST is accepted.
- `client_max_body_size 8k` — bounds the JSON payload.
- `proxy_ssl_verify off` — safe here because the target is loopback, no MITM surface.
- `Cookie`, `Authorization`, `X-Real-IP`, `X-Forwarded-*`, `Referer` headers are explicitly cleared before forwarding, so clients cannot spoof identity to bypass the plugin's rate limiter.
- Dedicated access/error logs at `/var/log/nginx/searcus_chat_{access,error}.log`.

The front-end widget (`assets/js/chat-terminal.js`) calls this endpoint same-origin, which is why there is no CORS config anywhere: the browser never talks to `evemilano.com` directly. To remove the chatbot entirely: delete the four asset tags from both `index.html` files AND comment out the `location = /api/chat` block from the vhost, then `sudo nginx -t && sudo systemctl reload nginx`.
