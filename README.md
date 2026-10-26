# Glypax website (glypax.com)

A static landing page: plain HTML + CSS, no JavaScript, no build step, no cookies and no third-party requests (the font is self-hosted).

## Deploying

Upload the **contents** of this folder to the web root of your server (the folder that should serve `index.html`), so that `https://glypax.com/` opens `index.html`.

```
index.html                             landing page
support/index.html                     https://glypax.com/support/  (Support URL for the app stores)
privacy-policy/index.html              https://glypax.com/privacy-policy/
terms-of-use/index.html                https://glypax.com/terms-of-use/
consumer-health-privacy-policy/index.html  https://glypax.com/consumer-health-privacy-policy/
404.html                               "page not found" page
assets/css/styles.css      styles
assets/fonts/              Figtree font (self-hosted, no Google Fonts)
assets/img/                logo, app screens, social preview image (og-image.png), app icons
favicon.ico, favicon.svg, apple-touch-icon.png, site.webmanifest
robots.txt, sitemap.xml
```

### 404 page
- **Apache / most shared hosting:** add `ErrorDocument 404 /404.html` to `.htaccess`
- **Nginx:** `error_page 404 /404.html;`
- **Netlify, Cloudflare Pages, GitHub Pages:** `404.html` is picked up automatically.

## Legal pages

Each legal page lives in its own folder as `index.html`, so the clean URLs work on any static host without rewrite rules (`/privacy-policy` redirects to `/privacy-policy/` automatically on Apache, Nginx and most hosts).

The document text is kept as in the source documents; only the markup was adapted to the site design (the documents' own links between each other now point to the new URLs). One deliberate wording change: in the Terms of Use, "dose calculations" was replaced with "estimated active medication levels", plus a sentence stating that the App does not calculate or recommend medication doses — update your source document to match. To update a policy, edit the text inside `<article class="container legal">` in the matching `index.html` and change the "Effective Date" line.

Use these URLs in App Store Connect, Google Play Console and inside the app:
- Support URL: https://glypax.com/support/
- Privacy Policy: https://glypax.com/privacy-policy/
- Terms of Use: https://glypax.com/terms-of-use/
- Consumer Health Data Privacy Policy: https://glypax.com/consumer-health-privacy-policy/

## Editing

- **Store links (once the app is live):** `index.html` has two `store-badge` blocks in the hero (`id="download"`), and every page has two more in its footer. For each one, change `<div class="store-badge" … role="img">` to `<a class="store-badge" href="STORE_URL">`, change the closing `</div>` to `</a>`, and remove `<span class="store-badge__soon">Coming soon</span>`.
- **"Works with popular GLP-1 medications" strip:** `index.html` contains six identical `marquee__list` lists — the copies keep the scrolling loop seamless on wide screens. Edit all six the same way. The list deliberately names only approved active ingredients (no brand names, no compounded or unapproved products) to keep app store review safe.
- **Colors:** CSS variables at the top of `assets/css/styles.css` (`--purple`, etc.).
- **Domain:** `glypax.com` appears in the canonical and social tags of every page, in `robots.txt` and in `sitemap.xml`.
- **Header and footer** are repeated in every page (`index.html`, `support/` and the three legal pages). If you change them, change all five.
- **Support email:** `support/index.html` (also used throughout the legal pages).

## Cookies

The site sets no cookies and has no analytics, so no cookie banner is needed. If you later add Google Analytics or any other tracker that uses cookies, you will need a consent banner.
