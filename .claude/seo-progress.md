# SEO Optimization Progress

## Completed (2026-02-10) — Score: 6.5 → ~8.5/10

### Head Meta Tags (index.html)
- [x] Fixed `og:image` to absolute URL
- [x] Added `og:image:width` / `og:image:height` (512x512)
- [x] Added Twitter Card tags (card, title, description, image)
- [x] Added `<link rel="canonical">`
- [x] Added `<meta name="robots" content="index, follow, max-image-preview:large">`
- [x] Added `<meta name="theme-color" content="#2d6a4f">`
- [x] Confirmed `lang="en"` already present

### Structured Data (index.html)
- [x] Organization schema (name, URL, logo, description, email)
- [x] SoftwareApplication schema (EducationalApplication, Free + Premium offers)

### Crawl Infrastructure
- [x] Created `sitemap.xml` (single entry, priority 1.0, lastmod 2026-02-10)
- [x] Created `robots.txt` (allow all, disallow Firebase configs, sitemap reference)
- [x] Created `404.html` (branded, noindex, matches site styling)

### Accessibility / SEO
- [x] Added `aria-hidden="true"` to all decorative SVGs (feature icons, checkmarks, denomination icons, phone nav, church building, hero email icon)

---

## Remaining Work — Score: 8.5 → 10/10

### HIGH IMPACT (→ 9.5)

#### 1. Image Optimization
The logo PNGs are ~1.38 MB each. This directly hurts LCP (Largest Contentful Paint).
- [ ] Convert `images/VineKinLogo.png` to WebP (target <50KB at 512x512)
- [ ] Create proper favicon set:
  - `favicon.ico` (32x32)
  - `apple-touch-icon.png` (180x180)
  - Optionally `favicon-16x16.png`, `favicon-32x32.png`
- [ ] Add `<link rel="apple-touch-icon" href="/apple-touch-icon.png">` to `index.html`
- [ ] Consider serving logo via `<picture>` with WebP + PNG fallback
- [ ] Update `404.html` favicon references too

#### 2. Font Loading Optimization
Google Fonts CSS is render-blocking, hurting FCP/LCP.
- [ ] Add `<link rel="preload" as="style">` for Google Fonts stylesheet
- [ ] Consider self-hosting fonts for faster delivery + fewer DNS lookups

#### 3. Web App Manifest
Signals proper web app to search engines, enables PWA install prompts.
- [ ] Create `site.webmanifest` with name, icons, theme_color, background_color
- [ ] Add `<link rel="manifest" href="/site.webmanifest">` to head

#### 4. Missing OG Tags
- [ ] Add `<meta property="og:site_name" content="VineKin">`
- [ ] Add `<meta property="og:locale" content="en_US">`

### MEDIUM IMPACT (→ 10)

#### 5. Firebase Hosting Headers (firebase.json)
Server-side headers improve security score, which search engines factor in.
- [ ] `Content-Security-Policy` header
- [ ] `X-Content-Type-Options: nosniff`
- [ ] `X-Frame-Options: DENY`
- [ ] `Strict-Transport-Security` (HSTS)
- [ ] Cache headers for static assets (images, fonts)
- [ ] Ensure `404.html` is configured as the custom error page

#### 6. Noscript Fallback
- [ ] Add `<noscript>` tag with basic content/message for users without JS
- [ ] Waitlist form won't work without JS — provide mailto fallback

#### 7. CSS Minification
Inline CSS is ~1300 lines (~30KB unminified).
- [ ] Minify before deploy (can be a build step or manual one-time)

#### 8. Sitemap Auto-Update
- [ ] Update `sitemap.xml` lastmod date on each deploy (could be a pre-deploy hook)

---

## Verification Checklist (run after all changes)
1. Open `index.html` locally — confirm no console errors
2. Validate structured data: https://validator.schema.org
3. Test OG/Twitter tags: https://www.opengraph.xyz
4. Google PageSpeed Insights: https://pagespeed.web.dev
5. Check 404 page on live site (navigate to non-existent path)
6. Mobile-Friendly Test: https://search.google.com/test/mobile-friendly
7. Lighthouse audit in Chrome DevTools (aim for 90+ on all categories)

## Image Conversion Commands (for reference)
```powershell
# Using cwebp (install via: scoop install libwebp)
cwebp -q 85 -resize 512 512 images/VineKinLogo.png -o images/VineKinLogo.webp

# Using ImageMagick (install via: scoop install imagemagick)
magick images/VineKinLogo.png -resize 180x180 apple-touch-icon.png
magick images/VineKinLogo.png -resize 32x32 favicon-32x32.png
magick images/VineKinLogo.png -resize 16x16 favicon-16x16.png
magick images/VineKinLogo.png -resize 32x32 favicon.ico
```
