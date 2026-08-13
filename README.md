# Evoque Living — Website Deploy Package

Static site, no build step. Everything the site needs is in this folder:

```
index.html                    the website (single page)
support.js                    runtime the page loads (keep next to index.html)
assets/                       all images
evoque-living-catalogue.pdf   catalogue download linked from the Enquire section
CNAME                         custom-domain marker for GitHub Pages (www.evoqueliving.com)
.nojekyll                     tells GitHub Pages to serve files as-is
```

## Deploy with GitHub Pages (10 minutes)

### A. Put the files on GitHub

Easiest (no command line):
1. Log in at github.com → **New repository** → name it e.g. `evoque-living-site`, Public → Create.
2. **Add file → Upload files** → drag the *contents* of this folder (not the folder itself) so `index.html` sits at the repo root → Commit.

Or with git:
```bash
cd deploy
git init && git add -A && git commit -m "Evoque Living site"
git branch -M main
git remote add origin https://github.com/<your-username>/evoque-living-site.git
git push -u origin main
```

### B. Turn on Pages
1. Repo → **Settings → Pages**.
2. Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
3. In ~1 minute the site is live at `https://<your-username>.github.io/evoque-living-site/`.

### C. Point evoqueliving.com at it
1. Settings → Pages → **Custom domain** → enter `www.evoqueliving.com` → Save.
   (The included CNAME file keeps this setting through future uploads.)
2. At your domain registrar (GoDaddy/Namecheap/etc), add DNS records:
   - `CNAME`  host `www` → `<your-username>.github.io`
   - For the bare domain `evoqueliving.com`, add four `A` records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. Back in Settings → Pages, tick **Enforce HTTPS** once the certificate is issued (can take 15–60 min after DNS propagates).

Done — https://www.evoqueliving.com serves the site.

## Alternatives
- **Netlify / Vercel**: drag-drop this folder in their dashboard, then add the custom domain in their domain settings (both issue HTTPS automatically).
- Any static host / ordinary web hosting: upload the folder contents to the web root via FTP.

## Updating the site
Replace the changed files in the repo (usually just `index.html` and anything new in `assets/`) and commit — Pages redeploys automatically in about a minute.

## Notes
- Keep `support.js`, `assets/` and the PDF in the same directory as `index.html`; paths are relative.
- The Enquire section's phone/WhatsApp/Instagram links are live; update them in `index.html` if contact details change.
