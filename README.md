# Bellini Bistro Italiano — Website

Static site for Bellini Bistro Italiano, BKK1, Phnom Penh.
Live at **https://bellinicambodia.com**

No build step. Plain HTML/CSS/JS — edit the files and upload.

## Local preview

The homepage and events page use `fetch('content.json')`, which browsers
block on `file://`. Serve over HTTP instead:

```bash
python3 -m http.server 8080
```

Then open http://localhost:8080

## Files

| File | Purpose |
|---|---|
| `index.html` | Homepage. Reads opening hours from `content.json`. |
| `about.html` `menu.html` `gallery.html` `reservations.html` `contact.html` | Static pages |
| `events.html` | Past events rendered from `content.json` |
| `guide.html` | Client-facing how-to-update guide |
| `content.json` | Editable content: `hours`, `deals`, `events`, `menu` |
| `style.css` | All styling |
| `images/` | Photos and logos |

## How content is edited

Edit `content.json` directly — it holds the menu, deals, opening hours and
past events. There is no admin UI; an `admin.html` editor panel existed
earlier and was removed.

`index.html` (hours), `events.html` (past events) and `menu.html` (all
dishes, headings and the promo strip) render from `content.json`. The one
exception is the pasta "Add-ons" row in `menu.html`, which has no
equivalent in the JSON schema and stays hard-coded — search for
`PASTA EXTRAS`.

## Known pending items

- [ ] **Deploy the current build.** The live site is an older version —
      every page differs and 14 images referenced here return 404 in
      production.
- [ ] **Google Analytics never activated** — `G-XXXXXXXXXX` is still a
      placeholder in all 7 pages.
- [ ] **`www.bellinicambodia.com` does not resolve** — no DNS record.
- [ ] **Ask Gabi to serve `404.html`.** The file deploys, but Caddy does
      not use it automatically the way Netlify or GitHub Pages would.
      Right now a missing URL returns a 404 with an empty body — a blank
      white page. The Caddyfile needs:

      ```
      handle_errors {
          rewrite * /404.html
          file_server
      }
      ```
