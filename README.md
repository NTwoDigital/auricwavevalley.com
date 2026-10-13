# auricwavevalley.com

Static website for Auricwave Valley, hosted free on GitHub Pages with DNS at Cloudflare.

## Files

| File | What it's for |
|---|---|
| `index.html` | The whole website — HTML, CSS and JS in one file. Edit this to change content. |
| `apps/car-expense-logbook/index.html` | The Car Expense Logbook product page, at `auricwavevalley.com/apps/car-expense-logbook/`. Self-contained like `index.html`. Screenshots, the app icon and the App Store badge load from Apple's servers. |
| `apps/notelio/index.html` | The Notelio product page, at `auricwavevalley.com/apps/notelio/`. Same layout and styles as the Car Expense Logbook page. |
| `404.html` | Shown when someone hits a URL that doesn't exist. |
| `privacy.html` | The privacy policy, at `auricwavevalley.com/privacy` (GitHub Pages serves `privacy.html` there without the extension). Linked from the footer of every page. |
| `terms.html` | The Terms of Use, at `auricwavevalley.com/terms`. Linked from the footer of every page. |
| `favicon.svg` | Browser tab icon — the wave mark in gold on near-black. |
| `logo-mark.svg` | The three-wave mark as scalable vector. Used inline in the header and footer. |
| `logo-mark.png` | Your original raster mark. |
| `logo-lockup-OLD-NAME.png` | Your original horizontal lockup. **It still reads "Auric Wave Valley"** — replace it with new artwork when you have it, then rename it to `logo-lockup.png`. |
| `og.png` | 1200x630 preview image shown when the site is shared on social or in chat apps. |
| `CNAME` | Tells GitHub Pages the site lives at `auricwavevalley.com`. Do not delete. |
| `robots.txt`, `sitemap.xml` | Search engine basics. |
| `.nojekyll` | Tells GitHub to serve the files as-is. |

---

## Part 1 — Put the site on GitHub

1. Sign in to GitHub and create a new **public** repository. Name it `auricwavevalley.com` (any name works).
2. On the repo page choose **Add file → Upload files**, drag in every file from this folder, and click **Commit changes**.
   - If `.nojekyll` won't upload from your file browser, use **Add file → Create new file**, type `.nojekyll` as the name, leave it empty, and commit.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
5. Wait about a minute, then check the temporary address GitHub shows you (`https://YOUR-USERNAME.github.io/auricwavevalley.com/`). The site should load.
6. Still in **Settings → Pages**, under **Custom domain**, enter `auricwavevalley.com` and click **Save**.

GitHub will now say the DNS check is in progress. That's expected — do Part 2 next.

---

## Part 2 — Point the domain at GitHub in Cloudflare

Open your domain in Cloudflare and go to **DNS → Records**. Delete any existing `A`, `AAAA` or `CNAME` record on the root (`@`) or on `www` first, then add these:

**Four A records for the root domain** — Type `A`, Name `@`:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**Four AAAA records for IPv6** (optional but recommended) — Type `AAAA`, Name `@`:

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**One CNAME for www** — Type `CNAME`, Name `www`, Target `YOUR-USERNAME.github.io`

### Important Cloudflare settings

- **Set the proxy status to "DNS only" (grey cloud) on all of the records above.** GitHub needs to see the real DNS to issue your HTTPS certificate. If the orange cloud is on, the certificate never gets issued.
- Go to **SSL/TLS → Overview** and set the encryption mode to **Full** (or **Full (strict)**). If it's on **Flexible**, the site will get stuck in a redirect loop.
- Once the site is live and HTTPS works, you can switch the proxy back on (orange cloud) if you want Cloudflare's caching. Keep SSL mode on Full if you do.

---

## Part 3 — Turn on HTTPS

DNS changes usually take 10–30 minutes (occasionally up to 24 hours). Once **Settings → Pages** shows the domain as verified, tick **Enforce HTTPS**. If the checkbox is greyed out, wait a bit longer, or remove and re-add the custom domain to force GitHub to re-issue the certificate.

`https://auricwavevalley.com` is now live.

---

## Editing the site later

Open `index.html` on GitHub and click the pencil icon. Commit, and the change is live in about a minute.

Things you'll probably want to change:

- **Legal pages** — `privacy.html` and `terms.html` share the same structure and styling. Each section is a `<section>` with an `id`, and the numbered list at the left links to those ids. If you add a section, add a matching entry to that list. Update the "Last modified" date near the top whenever either document changes.

  The terms were drafted for an Australian company selling consumer apps through the App Store. Two clauses in particular assume that: the Apple App Store section (required by Apple's own developer agreement if you distribute on iOS) and the Australian Consumer Law section. If you later distribute on Google Play or sell direct, those sections need revisiting.
- **Email addresses** — `info@auricwavevalley.com` appears twice in `index.html` (the contact section and the footer); `privacy@auricwavevalley.com` appears six times in `privacy.html`. It won't receive anything until the mailbox exists: Cloudflare Email Routing forwards an address at your domain to a personal inbox for free, under **Email → Email Routing** in your Cloudflare dashboard.
- **Company details** — the registered entity and ABN appear in the contact section and the footer. Update both if they change.
- **The three cards** under "What we build" — swap the placeholder categories for your real app names once they're ready.
- **Colours** — every colour is defined once at the top of the `<style>` block under `:root`. `--auric` is the gold accent.
- **Logo** — the header and footer draw the mark as inline SVG, so it stays sharp at any size and needs no image request. To adjust it, edit the three `<path d="M1 19 …">` lines. `logo-mark.svg` is the same artwork as a standalone file.
- **Brand gold** — `--auric: #d19a2e` is your logo gold, used for the mark, the hero waves and the accent rules. `--auric-deep: #8f6512` is a darkened version used only for small text and icons, where the lighter gold wouldn't be legible enough against white. Change both together if you shift the brand colour.
- **Social preview** — replace `og.png` with any 1200x630 image; the tag pointing at it is already in `<head>`.

## Previewing on your own computer

Just double-click `index.html` — it opens straight in a browser, no build step or server needed.
