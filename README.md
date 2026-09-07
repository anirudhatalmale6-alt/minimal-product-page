# Minimalist one-page product site

Plain HTML + CSS. No build step, no framework, no dependencies. Open
`index.html` in a browser and it works; upload the folder to any host and it
works there too.

```
site/
├── index.html      the whole page — all text lives here
├── styles.css      all styling
├── main.js         two small things: fade-in on scroll, footer year
├── README.md       this file
└── assets/
    ├── Inter.woff2                 body typeface (self-hosted = fast)
    ├── InstrumentSerif-400.woff2   headline typeface
    └── InstrumentSerif-400i.woff2  headline italic
```

---

## How to change things

Everything you would normally want to edit is in `index.html`, and every spot
is marked with a comment in CAPITALS. Search the file for the comment, change
the text between the tags, save, upload.

### 1 · The price

The price appears in **four** places (header, hero button, buy box, closing
bar). Each one is tagged `data-price`, so search `index.html` for:

```
data-price
```

…and replace `$00.00` in all four. That is the only place a price is stored —
there is no database.

### 2 · The Buy button / checkout link

There are four buy links, each marked:

```html
<!-- BUY LINK — replace "#" with your checkout URL -->
<a class="btn" href="#">Buy now …</a>
```

Replace `#` with your checkout URL:

- **Existing checkout** — paste the product URL exactly as it is.
- **Stripe** — Stripe Dashboard → Payment Links → create one → paste the
  `https://buy.stripe.com/...` link.
- **PayPal** — PayPal → Pay Links & Buttons → create → paste the link.

No keys, no server code, nothing to install. If you would rather have Stripe
Checkout open in an overlay instead of a new page, that is a small addition —
say the word.

### 3 · Product name, description, specs

| What | Where in `index.html` |
|---|---|
| Product name | under `<!-- PRODUCT NAME -->` |
| One-line positioning | under `<!-- POSITIONING LINE -->` |
| Two description paragraphs | under `<!-- DESCRIPTION -->` |
| The three benefit lines | under `<!-- THREE BENEFIT LINES -->` |
| Spec rows (Material, etc.) | under `<!-- SPEC TABLE -->` |
| Browser tab title + Google description | top of the file, `<!-- PAGE TITLE + SEO -->` |

Spec rows are just repeated blocks — copy a line to add a row, delete a line to
remove one. Nothing else has to change.

### 4 · Photos

Drop your images into `assets/` and swap each placeholder block:

```html
<figure class="plate plate-tall">…</figure>
```

for:

```html
<img src="assets/product-01.jpg" alt="Short description of the photo">
```

Suggested sizes — main shots **1400 × 1750** (portrait 4:5), thumbnails
**800 × 1000**. Export as JPG at ~80% quality, or WebP if your host supports it.
Keep each file under about 300 KB so the page stays fast.

### 5 · Colours and spacing

Top of `styles.css`, in the `:root` block. Change one value and it updates
everywhere:

```css
--paper: #FBFAF8;   /* page background   */
--ink:   #171613;   /* main text, button */
--line:  #E3DFD8;   /* hairline rules    */
--sec:   clamp(72px, 12vw, 168px);  /* space between sections */
```

---

## Publishing

Upload the contents of `site/` to your host's public folder (`public_html`,
`www`, or similar). That is the whole deployment. It also works as-is on
Netlify, Vercel, Cloudflare Pages, or GitHub Pages by dragging the folder in.

## Notes

- Responsive down to 320px wide; layout switches to a single column at 820px.
- Fonts are self-hosted, so the page makes no third-party requests at all.
- Respects `prefers-reduced-motion` — animations switch off for anyone who has
  that set in their OS.
