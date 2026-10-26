# Glypax — сайт (glypax.com)

Статичний сайт: HTML + CSS, без JavaScript, без збірки, без cookie і сторонніх запитів.

## Як залити

Скопіюй **вміст** цієї папки в корінь сайту на сервері (туди, де має лежати `index.html`), щоб `https://glypax.com/` відкривав `index.html`.

```
index.html                 головна сторінка
404.html                   сторінка "не знайдено"
assets/css/styles.css      стилі
assets/fonts/              шрифт Figtree (локально, без Google Fonts)
assets/img/                лого, скріни застосунку, OG-картинка для прев'ю, іконки
favicon.ico, favicon.svg, apple-touch-icon.png, site.webmanifest
robots.txt, sitemap.xml
```

### 404
- **Apache / більшість хостингів:** додай у `.htaccess` рядок `ErrorDocument 404 /404.html`
- **Nginx:** `error_page 404 /404.html;`
- **Netlify, Cloudflare Pages, GitHub Pages:** `404.html` підхоплюється автоматично.

## Що де міняти

- **Посилання на сторах, коли застосунок вийде:** у `index.html` два блоки `store-badge` у hero (`id="download"`) і два у футері. Заміни `<div class="store-badge" … role="img">` на `<a class="store-badge" href="ПОСИЛАННЯ">`, закрий `</a>` і прибери `<span class="store-badge__soon">Coming soon</span>`.
- **Список у стрічці "Works with every GLP-1":** у `index.html` два однакові списки `marquee__list` — другий потрібен для безшовної прокрутки, тож міняй обидва однаково.
- **Кольори:** змінні на початку `assets/css/styles.css` (`--purple` тощо).
- **Домен:** `glypax.com` вказаний у `index.html` (canonical, og:url, og:image), `robots.txt` і `sitemap.xml`.

## Cookie
Сайт не ставить cookie і не має аналітики, тому cookie-банер не потрібен. Якщо пізніше додаси Google Analytics або інші трекери з cookie — тоді знадобиться банер згоди.
