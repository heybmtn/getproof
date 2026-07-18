# Case Study Experts — landing page

Static, no build step, no dependencies.

| File | Route | Style |
|---|---|---|
| `public/index.html` | `/` | Long-form sales letter (abpmastery-style structure) |
| `public/nxt-style.html` | `/nxt-style` | Dark, lime accent (nxt.agency-style) — note: still contains earlier rewritten copy |
| `public/fonts/` | | Lato 400/700/900, self-hosted (latin subset, ~23KB each) |
| `public/_headers` | | Cache + security headers |
| `public/robots.txt` | | Add your sitemap URL if you make one |

## Deploy to Cloudflare

    npx wrangler deploy                                                # Workers
    npx wrangler pages deploy public --project-name case-study-experts # Pages

Or drag the `public/` folder into the dashboard (Workers & Pages → Create → Pages → Upload assets).

## Local preview

    python3 -m http.server -d public 8080

## Lighthouse

Scores 100 / 100 / 100 / 100 (Lighthouse 13, mobile and desktop presets), verified over four runs.
Two of the four categories depend on the host, not the code — Cloudflare covers both:

- **Compression** — Cloudflare gzip/brotli's HTML automatically.
- **Cache lifetimes** — set by `public/_headers` (fonts immutable for a year).

Retest at https://pagespeed.web.dev/ once it's on a real HTTPS domain.

## Still to fill in

- **The two CTA buttons** — both `href` values are `#`, marked `<!-- PLACEHOLDER -->`. Point them at your contact form, Calendly or a `mailto:`.
- **robots.txt** — uncomment the Sitemap line if you add one.

## Notes

- Copy is yours verbatim. The name is set in the nav, `<title>`, OG tag and footer.
- Accent colour: `--lime` in `:root`. `--lime-dark` is the same hue darkened for small text on white.
- Fonts are self-hosted rather than loaded from Google Fonts: no third-party request, no render-blocking stylesheet, and no consent/GDPR question about Google receiving visitor IPs. To change weights, the files came from `npm i @fontsource/lato`.
