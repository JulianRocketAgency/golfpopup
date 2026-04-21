# GolfPopup.nl

Officiële website voor [GolfPopup.nl](https://www.golfpopup.nl) — verhuur van professionele mobiele golfsimulators voor evenementen in Nederland.

## Structuur

```
golfpopup/
├── index.html        # Volledige single-page website (alle pagina's via JS routing)
├── sitemap.xml       # XML sitemap voor zoekmachines
├── robots.txt        # Crawl-instructies voor zoekmachines
├── .htaccess         # Apache: HTTPS redirect, GZIP, caching, security headers
└── README.md         # Dit bestand
```

## Pagina's

De site is een single-page application (SPA) — alle content zit in `index.html` en navigatie werkt via JavaScript. Dit is bewust gekozen voor eenvoudige hosting zonder server-side routing.

| Sectie / Pagina           | ID in HTML                  |
|---------------------------|-----------------------------|
| Homepage                  | `#home`                     |
| De Simulator              | `#simulator`                |
| Gelegenheden              | `#occasions`                |
| Tarieven                  | `#pricing-page`             |
| FAQ                       | `#faq`                      |
| Blog overzicht            | `#blog`                     |
| Golfsimulator huren       | `#golfsimulator-huren`      |
| Golfsimulator evenement   | `#golfsimulator-evenement`  |
| Garmin R50                | `#garmin-r50`               |
| Gelderland                | `#gelderland`               |
| Bedrijfsdag               | `#bedrijfsdag`              |
| Blog: Thuis huren         | `#blog-golfsimulator-thuis` |
| Blog: Beste golfbanen     | `#blog-beste-golfbanen`     |
| Blog: Teambuilding        | `#blog-teambuilding`        |
| Blog: Bruiloft            | `#blog-bruiloft`            |
| Blog: Garmin R50 review   | `#blog-garmin-review`       |

## Deployment

### Apache (bijv. TransIP, Antagonist, DirectAdmin)

1. Upload alle bestanden naar de `public_html` of `www` map
2. Zorg dat `mod_rewrite`, `mod_deflate` en `mod_expires` actief zijn (standaard bij de meeste hostingproviders)
3. Controleer HTTPS-certificaat (Let's Encrypt of hosting-eigen SSL)
4. Dien sitemap in bij [Google Search Console](https://search.google.com/search-console) en [Bing Webmaster Tools](https://www.bing.com/webmasters)

### Vercel / Netlify (statisch)

Als u Vercel of Netlify gebruikt, vervang `.htaccess` door de respectievelijke config:

**Netlify (`netlify.toml`):**
```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "SAMEORIGIN"
    X-Content-Type-Options = "nosniff"
    Strict-Transport-Security = "max-age=31536000; includeSubDomains"
```

**Vercel (`vercel.json`):**
```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Frame-Options", "value": "SAMEORIGIN" },
        { "key": "X-Content-Type-Options", "value": "nosniff" }
      ]
    }
  ]
}
```

## Na deployment te doen

- [ ] KvK en BTW-nummer invullen in footer (`index.html`, zoek op `[invullen]`)
- [ ] Telefoonnummer toevoegen in contact-sectie en JSON-LD (`"telephone": ""`)
- [ ] Echte foto's toevoegen (hero, equipmentsecties) en verwijzen in `og:image`
- [ ] Google Analytics of Matomo tag toevoegen in `<head>` (voor Matomo: privacy-vriendelijk)
- [ ] Google Search Console verifiëren en sitemap indienen
- [ ] Bing Webmaster Tools verifiëren en sitemap indienen
- [ ] Social media links toevoegen in footer en JSON-LD `sameAs`
- [ ] Favicon PNG aanmaken (512×512) als vervanging voor de inline SVG data-URI
- [ ] Meta og:image aanmaken (1200×630 px) en uploaden als `og-image.jpg`

## SEO-checklist

- [x] Unieke `<title>` en `<meta description>` per pagina (dynamisch via JS)
- [x] Open Graph tags (Facebook/LinkedIn)
- [x] Twitter Card tags
- [x] JSON-LD structured data: LocalBusiness, WebSite, FAQPage, BreadcrumbList, Offers
- [x] `robots.txt` met sitemap-verwijzing
- [x] `sitemap.xml` met alle pagina's en prioriteiten
- [x] Geo-meta tags (regio Gelderland)
- [x] Canonical URL per pagina
- [x] `lang="nl"` op `<html>`
- [x] Semantische HTML: `<main>`, `<nav>`, `<footer>`, heading-hiërarchie
- [x] Skip-to-content link (toegankelijkheid)
- [x] HTTPS-redirect via `.htaccess`
- [x] GZIP-compressie via `.htaccess`
- [x] Browser caching via `.htaccess`
- [x] Security headers via `.htaccess`
- [ ] Core Web Vitals optimaliseren na deployment (controleer via PageSpeed Insights)
- [ ] Afbeeldingen in WebP-formaat + `loading="lazy"` als echte foto's worden toegevoegd

## Contact

📧 info@golfpopup.nl  
📍 Otterlo, Gelderland
