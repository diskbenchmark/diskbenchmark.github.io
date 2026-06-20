# Disk Benchmark Website — Deploy ke GitHub Pages

Website statik klasik untuk tool **Disk Benchmark (D-Bench)**.

> Target domain: **https://diskbenchmark.github.io/**

---

## 1. Struktur file

```
.
├── index.html              # Beranda (download + FAQ + SEO lengkap)
├── help.html               # Dokumentasi pengguna
├── 404.html                # Halaman 404 (noindex)
├── style.css               # Stylesheet klasik terpusat (responsive + print + a11y)
├── robots.txt              # Crawler directives + sitemap pointer
├── sitemap.xml             # Sitemap untuk Google Search Console
├── site.webmanifest        # PWA manifest
├── .nojekyll               # Bypass Jekyll processing di GitHub Pages
├── _config.yml             # Konfigurasi GitHub Pages (opsional)
│
├── logo.png                # Logo utama (100x100 PNG, dari base64 asli)
├── logo.svg                # Versi SVG untuk mask-icon Safari
├── favicon.ico             # Favicon legacy
├── favicon-16x16.png       # Favicon modern
├── favicon-32x32.png
├── apple-touch-icon.png    # 180x180 untuk iOS
├── android-chrome-192x192.png
├── android-chrome-512x512.png
├── mstile-150x150.png      # Windows tile
├── og-image.png            # 1200x630 untuk Open Graph / Twitter Card
│
├── view1.PNG               # Screenshot main window
├── view2.PNG               # Screenshot settings window
├── viewdefault.PNG         # Preview tema Default
├── viewblue.PNG            # Preview tema Blue
├── viewred.PNG             # Preview tema Red
│
└── files/                  # File installer .exe
    ├── DiskBenchmark-1.0-Default(EN).exe
    ├── DiskBenchmark-1.0-Blue(EN).exe
    ├── DiskBenchmark-1.0-Red(EN).exe
    └── wvista7/
        ├── DiskBenchmark-1.0-Vista7-Default(EN).exe
        ├── DiskBenchmark-1.0-Vista7-Blue(EN).exe
        └── DiskBenchmark-1.0-Vista7-Red(EN).exe
```

## 2. Cara deploy ke GitHub Pages

### Opsi A — Buat repo `diskbenchmark.github.io`

1. Buat repository baru di GitHub dengan nama **tepat**:
   `diskbenchmark.github.io`
   (harus persis sama dengan username/organisasi pemilik repo).
2. Upload semua isi folder ini ke branch `main` (root repo):
   ```bash
   cd dbech-web-improved
   git init
   git add .
   git commit -m "Initial commit - Disk Benchmark website"
   git branch -M main
   git remote add origin https://github.com/diskbenchmark/diskbenchmark.github.io.git
   git push -u origin main
   ```
3. Buka **Settings → Pages**. Source: `Deploy from a branch`, branch: `main`, folder: `/ (root)`.
4. Tunggu 1–2 menit. Site live di **https://diskbenchmark.github.io/**.

### Opsi B — Pakai repo biasa, publish dari folder `/docs` atau `/`

Jika Anda sudah punya repo dan tidak ingin repo khusus `<user>.github.io`:
1. Letakkan file-file ini di folder `docs/` (atau root) repo.
2. Settings → Pages → Source: `Deploy from a branch`, branch: `main`, folder: `/docs`.
3. Site akan live di `https://<username>.github.io/<repo>/`.
   **Catatan:** Jika path tidak root, ubah semua URL di `index.html` / `help.html` / `sitemap.xml` / `robots.txt` dari `https://diskbenchmark.github.io/` ke `https://<username>.github.io/<repo>/`.

## 3. Setup SEO tambahan (disarankan)

### Google Search Console
1. Buka https://search.google.com/search-console
2. Add property → URL prefix → `https://diskbenchmark.github.io/`
3. Verifikasi kepemilikan (paling mudah: upload file HTML verifikasi ke root repo, atau pakai GitHub Pages + meta tag).
4. Submit **sitemap.xml**: `https://diskbenchmark.github.io/sitemap.xml`
5. Request indexing untuk `https://diskbenchmark.github.io/` dan `https://diskbenchmark.github.io/help.html`.

### Bing Webmaster Tools
1. Buka https://www.bing.com/webmasters
2. Add site → submit sitemap yang sama.

### Open Graph preview tester
- https://www.opengraph.xyz/url/https%3A%2F%2Fdiskbenchmark.github.io%2F
- https://developers.facebook.com/tools/debug/

### Twitter Card validator
- https://cards-dev.twitter.com/validator

### Schema validator
- https://search.google.com/test/rich-results
  (paste URL → akan mengecek SoftwareApplication, FAQPage, TechArticle, BreadcrumbList)

### Lighthouse audit
- Buka site di Chrome → DevTools → Lighthouse → Run.
- Target: 90+ untuk Performance, Accessibility, Best Practices, SEO.

## 4. Optimasi SEO yang sudah dilakukan

### Meta tags
- ✅ Title SEO-friendly dengan keyword utama di awal
- ✅ Meta description 130–160 karakter
- ✅ Meta keywords (Google mengabaikan tapi Bing/Yandex masih pakai)
- ✅ Meta robots: `index, follow, max-image-preview:large`
- ✅ Canonical URL di setiap halaman → `https://diskbenchmark.github.io/...`
- ✅ hreflang `en` + `x-default`

### Open Graph (Facebook, LinkedIn, WhatsApp, Discord)
- ✅ `og:type` (website / article)
- ✅ `og:url`, `og:title`, `og:description`
- ✅ `og:image` 1200x630 dengan dimensi eksplisit
- ✅ `og:site_name`, `og:locale`
- ✅ `article:published_time`, `article:modified_time` (help.html)

### Twitter Card
- ✅ `twitter:card` = `summary_large_image` (index, help) / `summary` (404)
- ✅ `twitter:title`, `twitter:description`, `twitter:image`

### Structured Data (JSON-LD)
- ✅ `WebSite` schema + SearchAction (index)
- ✅ `SoftwareApplication` schema + Offer (free) + FeatureList + Screenshots (index)
- ✅ `FAQPage` schema dengan 5 Q&A (index)
- ✅ `TechArticle` schema (help)
- ✅ `BreadcrumbList` schema (index, help, 404)

### File infrastruktur
- ✅ `robots.txt` — allow all, link ke sitemap, disallow `/files/` (exe tidak perlu diindeks)
- ✅ `sitemap.xml` — 3 URL dengan priority & changefreq
- ✅ `site.webmanifest` — PWA ready (theme color, icons, shortcuts)
- ✅ `.nojekyll` — bypass Jekyll processing
- ✅ `_config.yml` — konfigurasi minimal GitHub Pages

### Favicon set lengkap
- ✅ `favicon.ico` (legacy)
- ✅ `favicon-16x16.png`, `favicon-32x32.png` (modern browsers)
- ✅ `apple-touch-icon.png` 180x180 (iOS)
- ✅ `android-chrome-192x192.png`, `android-chrome-512x512.png` (PWA)
- ✅ `mstile-150x150.png` (Windows tile)
- ✅ `logo.svg` (mask-icon Safari pinned tab)

### Heading hierarchy
- ✅ Tepat 1 `<h1>` per halaman
- ✅ `<h2>` untuk section, `<h3>` untuk sub-section
- ✅ Skip-link untuk a11y

### Image optimization
- ✅ Semua `<img>` punya `alt` deskriptif
- ✅ `width` dan `height` eksplisit (mencegah layout shift / CLS)
- ✅ `loading="lazy"` untuk screenshot di bawah fold

### Aksesibilitas (juga meningkatkan SEO)
- ✅ Skip-to-content link
- ✅ Focus ring terlihat (keyboard navigation)
- ✅ `aria-label` untuk footer navigation
- ✅ `<caption>` (visually-hidden) untuk tabel download
- ✅ Kontras warna AA (link biru di latar putih = 8.6:1)

### Konten SEO-friendly
- ✅ Paragraf intro deskriptif di homepage
- ✅ Section "About Disk Benchmark" dengan kata kunci natural
- ✅ FAQ accordion (5 pertanyaan umum dengan keyword long-tail)
- ✅ Footer navigation internal (Home / Docs / Download / Support)

## 5. Catatan tentang domain

Karena target adalah `diskbenchmark.github.io` (bukan custom domain), **tidak perlu file CNAME**. File CNAME hanya dibutuhkan jika Anda pakai custom domain seperti `diskbench.com`. Jika nanti ingin custom domain:
1. Buat file `CNAME` (tanpa ekstensi) berisi domain Anda, mis. `diskbench.com`
2. Setup DNS A record atau CNAME di provider domain Anda mengarah ke GitHub Pages.

## 6. Update konten di masa depan

Untuk update `dateModified` di JSON-LD saat Anda memperbarui halaman:
- `index.html`: ubah `"dateModified": "2026-06-20"` ke tanggal update terbaru.
- `help.html`: ubah `"dateModified"` di meta tag dan JSON-LD.
- `sitemap.xml`: ubah `<lastmod>` ke tanggal update.

Halaman yang sudah lama tidak diupdate akan tetap diindeks, tapi update reguler (sekali per kuartal) membantu Google memprioritaskan konten Anda.

---

© 2026 Ari Sohandri Putra. All Rights Reserved.
