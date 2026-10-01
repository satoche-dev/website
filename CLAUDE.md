# satoche-web

The landing page of Satoche, a macOS app that prepares the French crypto tax declaration on the
user's computer. "Satoche" is a working name. Read the [README](README.md) first.

## Rules for every change

1. **The page collects nothing.** No cookie, no tracker, no analytics, no form, no email, no
   third-party font, script, image or request. Keep the Content-Security-Policy meta tag strict.
2. **Every claim about competitors or incidents is dated and sourced**, in the footnotes of the page.
   Never name a competitor in the copy. No absolute claim ("100 % secure", "unhackable").
3. **Copy in French, "vous".** Say *assistant fiscal en ligne* for the competitors, never
   *déclarer en ligne*: every declaration is made on impots.gouv.fr.
4. **Say it positively**: what the user keeps, not what we lack.
5. **One text style per block**: same size, same weight, one accent at most, in colour.
6. **The message is broad** (computer, crypto, exchange). Mac, Bitcoin, France and the first exchange
   appear only in the "première version" section.
7. Colours are the tokens at the top of `public/index.html`. Light and dark themes both work.
8. Check each change in a browser at 375 px and at desktop width, with no console error and no
   horizontal scroll.

## Files

- `public/` is what GitHub Pages publishes, on each push to `main`.
- `drafts/` holds local design explorations. Git ignores it.
- Preview: `python3 -m http.server 4321 --bind 127.0.0.1 --directory public`

## Workflow

- Commits and pull requests in English. This repository is public: never commit anything internal.
