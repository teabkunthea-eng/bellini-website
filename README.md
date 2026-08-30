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
| `admin.html` | CMS panel — edits `content.json`, downloads the result |
| `guide.html` | Client-facing how-to-update guide |
| `content.json` | Editable content: `hours`, `deals`, `events`, `menu` |
| `style.css` | All styling |
| `images/` | Photos and logos |

## How the CMS works

`admin.html` edits content and downloads a new `content.json`, which you
then replace in this folder and re-upload. It is client-side only — the
login is a JavaScript check, not real authentication. Keep this repo
private.

## Known pending items

- [ ] **Deploy the current build.** The live site is an older version —
      every page differs and 14 images referenced here return 404 in
      production.
- [ ] **`admin.html` is not deployed** (404 on live).
- [ ] **`menu.html` does not read `content.json`.** The admin panel edits
      `menu` and `deals`, but nothing consumes them, so those edits have
      no effect. Only `index.html` (hours) and `events.html` are wired up.
- [ ] **Google Analytics never activated** — `G-XXXXXXXXXX` is still a
      placeholder in all 7 pages.
- [ ] **`www.bellinicambodia.com` does not resolve** — no DNS record.
- [ ] **`guide.html` may have wrong deploy instructions.** It describes
      Netlify drag-and-drop, but the live server reports Caddy. Confirm
      the actual host before handing the guide to the client.
- [ ] Stale comments in `sitemap.xml` and `robots.txt` ("UPDATE the
      domain once live") — URLs are correct, just leftover notes.
