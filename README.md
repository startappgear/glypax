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
robots.txt, sitemap.xml, llms.txt (summary for AI assistants)
```

### 404 page
- **Apache / most shared hosting:** add `ErrorDocument 404 /404.html` to `.htaccess`
- **Nginx:** `error_page 404 /404.html;`
- **Netlify, Cloudflare Pages, GitHub Pages:** `404.html` is picked up automatically.

## Legal pages

Each legal page lives in its own folder as `index.html`, so the clean URLs work on any static host without rewrite rules (`/privacy-policy` redirects to `/privacy-policy/` automatically on Apache, Nginx and most hosts).

The document text is kept as in the source documents; only the markup was adapted to the site design (the documents' own links between each other now point to the new URLs). Deliberate wording changes (update your source documents to match):
- **All three documents:** deletion steps now read "Profile → Clear All Data" (Terms of Use and Consumer Health Data Privacy Policy previously said "in the App's settings").
- **Consumer Health Data Privacy Policy:** Effective Date updated to October 27, 2026.
- **Terms of Use (effective October 27, 2026):** "dose calculations" was replaced with "estimated active medication levels", plus a sentence stating that the App does not calculate or recommend medication doses.
- **Privacy Policy (effective October 27, 2026):** removed every statement that an age bracket or gender is sent to analytics (Profile Data row, Analytics Data row, GDPR consent bullet), and stated that analytics events never contain profile details. Profile data is described as stored on the device only. Added a "How to Delete Your Data" section (`#data-deletion`) with deletion steps and what is kept (kept data is deleted automatically; no deletion-on-request promise). Also removed the promise that analytics consent can be withdrawn in the App's settings (the app has no such toggle); analytics relies on legitimate interests. To update a policy, edit the text inside `<article class="container legal">` in the matching `index.html` and change the "Effective Date" line.

Use these URLs in App Store Connect, Google Play Console and inside the app:
- Support URL: https://glypax.com/support/
- Data deletion URL (Google Play Data safety): https://glypax.com/privacy-policy/#data-deletion
- Privacy Policy: https://glypax.com/privacy-policy/
- Terms of Use: https://glypax.com/terms-of-use/
- Consumer Health Data Privacy Policy: https://glypax.com/consumer-health-privacy-policy/

## Editing

- **Store links:** Google Play is live (`https://play.google.com/store/apps/details?id=com.glypax.tracker`): the badge is an `<a class="store-badge store-badge--live" …>` in the hero of `index.html` and in every page's footer (5 places). The App Store badge is still "Coming soon". When the iOS app is live, do the same for its 5 badges: change `<div class="store-badge" … role="img">` to `<a class="store-badge store-badge--live" href="APP_STORE_URL" target="_blank" rel="noopener" aria-label="Download Glypax on the App Store">`, change the closing `</div>` to `</a>`, and remove `<span class="store-badge__soon">Coming soon</span>`. Then update the "coming soon to iOS" wording in the `index.html` meta/social descriptions, the FAQ, the JSON-LD (`operatingSystem`, `sameAs`) and `llms.txt`.
- **"Works with popular GLP-1 medications" strip:** `index.html` contains six identical `marquee__list` lists — the copies keep the scrolling loop seamless on wide screens. Edit all six the same way. This strip is still hidden; the visible "Works with all popular GLP-1 medications" section (`#medications`) replaced it.
- **Medication brand names:** the home page, FAQ, JSON-LD and `llms.txt` name brands (Ozempic®, Wegovy®, Mounjaro® …) next to their active ingredients, always with ® and the trademark/non-affiliation note under the medications list. Keep that note in sync if you add a brand. Keep brand names out of the store listing title and icon.
- **AI and search visibility:**
  - `index.html` `<head>` has one JSON-LD `@graph` (WebSite, Organization, MobileApplication, FAQPage). The FAQPage text must match the visible FAQ (`#faq`) word for word, so edit both together.
  - `llms.txt` (site root) is a plain-Markdown summary of the app for AI assistants. Update it when features, pricing, platforms or medications change.
  - `robots.txt` explicitly allows all search and AI crawlers.
  - After deploying, submit `sitemap.xml` in Google Search Console and Bing Webmaster Tools (ChatGPT search and Copilot use Bing's index), and bump `<lastmod>` in `sitemap.xml` when a page changes.
- **Colors:** CSS variables at the top of `assets/css/styles.css` (`--purple`, etc.).
- **Domain:** `glypax.com` appears in the canonical and social tags of every page, in `robots.txt` and in `sitemap.xml`.
- **Header and footer** are repeated in every page (`index.html`, `support/` and the three legal pages). If you change them, change all five.
- **Support email:** `support/index.html` (also used throughout the legal pages).

## Cookies

The site sets no cookies and has no analytics, so no cookie banner is needed. If you later add Google Analytics or any other tracker that uses cookies, you will need a consent banner.
