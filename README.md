# Satoche website

The landing page of Satoche, a macOS app that prepares the French crypto tax declaration on the
user's computer. "Satoche" is a working name (trademark not cleared).

## Files

Only `public/` is published.

| File | Content |
| --- | --- |
| `public/index.html` | The page. Self-contained: styles and scripts inline. |
| `public/feed.xml` | The Atom feed for release news. |
| `public/logo.svg` | The Satoche mark (for dark backgrounds). |

`drafts/` holds local design explorations. Git ignores it.

## Rules

The page practises what the product promises:

- No cookie, no tracker, no third-party font, script or request. The Content-Security-Policy in
  `index.html` enforces it.
- No personal data collected: no sign-up form, no email.
- Every claim about competitors or incidents is dated and has a source, and names no company.

The brand and the market analysis live in the app repository: `docs/brand.md` and
`docs/market/competitors.md`.

## Before the public launch

- A lawyer reviews the comparative claims and the legal notice.
- Set `SIMPLEX_LINK` and check `RELEASE_DATE` in the script of `index.html`.
- Remove the `noindex` from the `robots` meta tag in `public/index.html`.
- Choose the domain.

## Preview

```bash
python3 -m http.server 4321 --bind 127.0.0.1 --directory public
```

## Deployment

GitHub Pages, from `.github/workflows/pages.yml`: each push to `main` publishes `public/`.

The repository is public on purpose: anyone can check that the page has no tracker, no cookie and no
third-party request.

GitHub Pages sets no custom HTTP headers. The security policy and the `noindex` live in the page, as
meta tags.
