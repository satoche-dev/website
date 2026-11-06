# Satoche website

> **Read-only mirror.** The public repository `satoche-dev/website` is a subtree split of `website/`
> in the private Satoche monorepo. Change the files in the monorepo. The mirror takes no pull
> requests: use its issues to contact us.

The landing page of Satoche, a macOS app that prepares the French crypto tax declaration on the
user's computer.

## Files

GitHub Pages serves only `public/`. The `main` branch of the mirror holds all of `website/`.

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

The monorepo is private, so the page is served from a public mirror, `satoche-dev/website`. On each
push to `main` that changes `website/`, the root `.github/workflows/pages.yml` updates two branches of
the mirror:

- `gh-pages`: a copy of `website/public/`, which GitHub Pages serves.
- `main`: `git subtree split --prefix=website`, with a force push.

Never edit the mirror by hand: the next publish overwrites it.

The split makes public the message, the author and committer names and emails, and the dates of
each commit that changes `website/`, old commits included. Commit with an email that you accept to
make public. Keep
website changes in their own commits, and write nothing internal in their messages.

The mirror is public on purpose: anyone can check that the page has no tracker, no cookie and no
third-party request.

One-time setup:

1. Create an SSH key pair with no passphrase: `ssh-keygen -t ed25519 -N '' -f deploy_key`.
2. Add `deploy_key.pub` to `website` (Settings, Deploy keys) with write access.
3. Save the content of `deploy_key` as the secret `WEBSITE_DEPLOY_KEY` in `satoche` (Settings, Secrets
   and variables, Actions). Then delete both local files.
4. In `website`, set Pages to deploy from branch `gh-pages`, folder `/ (root)`, with the custom
   domain `satoche.dev`.
5. In `website`, disable pull requests and mark the repository as a mirror:
   `gh api -X PATCH repos/satoche-dev/website -F has_pull_requests=false -f description='Web landing page. READONLY SUBTREE SPLIT of website/ in the satoche monorepo.'`

GitHub Pages sets no custom HTTP headers. The security policy and the `noindex` live in the page, as
meta tags.
