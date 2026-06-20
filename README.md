# fjbuilds.com

Landing page for builds page — AI Automation for Local Business.

- `index.html` — the entire site (single self-contained file, no build step)
- `business-card.md` — business card spec for the printer
- `CNAME` — custom domain for GitHub Pages (created during deploy)

## Before going live

1. **Calendly link** — replace `https://calendly.com/REPLACE-ME` in `index.html`
   (two spots) with your real 20-minute-call booking link.
2. **Phone** — optional to add anywhere on the page; it's on the card instead.

## Deploy (GitHub Pages)

```bash
cd /Users/fjunior/dev/fjbuilds
git init -b main
git add .
git commit -m "Initial landing page"
gh repo create fjbuilds --public --source=. --push
gh api -X POST repos/{owner}/fjbuilds/pages -f source[branch]=main -f source[path]=/
```

Then point the domain (see below). Pages serves from the repo root on `main`.

## Custom domain (fjbuilds.com)

1. A `CNAME` file containing `fjbuilds.com` lives in the repo root (Pages reads it).
2. In **Porkbun DNS**, add these records:

   | Type  | Host  | Answer / Value          |
   |-------|-------|-------------------------|
   | A     | (root / @) | 185.199.108.153    |
   | A     | (root / @) | 185.199.109.153    |
   | A     | (root / @) | 185.199.110.153    |
   | A     | (root / @) | 185.199.111.153    |
   | CNAME | www   | <your-github-username>.github.io |

3. In the repo on github.com → **Settings → Pages**, set the custom domain to
   `fjbuilds.com` and enable **Enforce HTTPS** (after the cert provisions, ~15 min).

DNS can take 15 min–24 hr to propagate. HTTPS appears once GitHub validates the domain.

## Updating the page later

```bash
cd /Users/fjunior/dev/fjbuilds
# edit index.html
git add index.html && git commit -m "Update copy" && git push
```

Live within a minute or two of pushing.
