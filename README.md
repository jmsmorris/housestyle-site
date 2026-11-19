# Housestyle Co. — site

A single-page static site. No build step, no dependencies to install — it's one `index.html` file with everything embedded (styles, fonts loaded from Google Fonts, a tiny script for the footer year).

## Files

- `index.html` — the whole site
- `README.md` — this file

## Before you deploy

1. **Replace the placeholder contact info.** Search the file for `hello@housestyle.ca` (appears twice) and swap in your real email once you've registered a domain.
2. **Forms are HubSpot embedded forms.** The contact form (`index.html`) and the free-template signup (`free-template/index.html`) load HubSpot's form embed (portal `343915332`, region `na3`). Form IDs are in each page's `hbspt.forms.create` call. HubSpot draws the forms inside an iframe, so their look (colours, fonts, buttons) is set in HubSpot's form editor under the Style tab, not in `style.css`. Fields, labels, Captcha and notifications are managed there too. After a successful submit, the free-template page listens for HubSpot's submit message and sends the visitor to the PDF.
3. **Domain.** Once you've confirmed availability (see your registrar search), point it at wherever you deploy.

## Deploy it — pick one

### Option A: Vercel (matches your LEDGR setup)
1. Go to [vercel.com](https://vercel.com) and sign in (GitHub login is easiest).
2. Click **Add New → Project**.
3. Either connect a GitHub repo containing this folder, or use the Vercel CLI:
   ```bash
   npm i -g vercel
   cd housestyle-site
   vercel
   ```
4. Follow the prompts — no build settings needed, it'll detect a static site automatically.
5. Add your custom domain under **Project → Settings → Domains**.

### Option B: Netlify (drag-and-drop, no CLI needed)
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the `housestyle-site` folder straight into the browser window.
3. It deploys instantly with a free `*.netlify.app` URL. Add your custom domain under **Site settings → Domain management**.

### Option C: GitHub Pages (free, if you're already using GitHub)
1. Push this folder to a GitHub repo.
2. Repo **Settings → Pages → Deploy from a branch → main → / (root)**.
3. Your site is live at `https://<username>.github.io/<repo>/`. Add a custom domain under the same Pages settings.

## SEO — what's already built in

- Descriptive `<title>` and meta description targeting "writing style guide," "nonprofit communications," and "sport organization communications"
- Open Graph and Twitter Card tags (so links look right when shared on LinkedIn/social)
- `robots.txt` and `sitemap.xml` — both point at `https://housestyle.ca/`, update the domain in both files once you've registered one
- JSON-LD structured data (`ProfessionalService` schema) — helps Google understand what the business is and who it serves, and is a prerequisite for rich results
- Proper heading hierarchy: one `<h1>` (the "housestyle" headword), `<h2>` for each major section, `<h3>` for sub-items — search engines weight real heading tags, not just styled text
- Semantic HTML landmarks (`<header>`, `<nav>`, `<main>`, `<footer>`) instead of generic `<div>`s
- `preconnect` hints for Google Fonts to speed up first paint (page speed is a ranking factor)

## SEO — what you still need to do once it's live

1. **Register the real domain** and do a find-and-replace for every `housestyle.ca` placeholder in `index.html`, `robots.txt`, and `sitemap.xml`.
2. **Make a real `og-image.png`** (1200×630px) and drop it in the site root — right now the Open Graph tags point to an image that doesn't exist yet, so social shares won't show a preview image until you add one.
3. **Submit to Google Search Console** ([search.google.com/search-console](https://search.google.com/search-console)) — verify the domain, submit `sitemap.xml`, and request indexing. This is the single highest-leverage thing you can do; without it, Google may take weeks to find the site on its own.
4. **Add a few backlinks** — CharityVillage's actual offering is a free sector directory for nonprofit organizations (email-in listing, not a consultant directory), so that's not a fit here. Better options: an ONN member profile, a LinkedIn Services listing, or a mention on your personal site (jacobmorris.ca).
5. **Content over time** — a static one-pager will only rank for a handful of terms. If you want to rank for things like "how to build a nonprofit style guide," that needs blog-style pages, which means moving beyond a single `index.html` file (a static site generator or a `/blog` folder of individual pages would both work).

## The free template / lead magnet (`free-template/`)

- `free-template/index.html` — the gated landing page (email capture form)
- `free-template/thank-you.html` — the download page, revealed after signup
- `free-template/Housestyle-Co-Style-Guide-Starter-Template.pdf` — the actual template

### Important: this isn't really gated yet

A static site has no server, so there's no way for `index.html` to actually check that someone submitted the form before letting them reach `thank-you.html` — right now, anyone who guesses or is given the `thank-you.html` URL directly can download the PDF without ever entering an email. The form redirects to the PDF only after HubSpot confirms the submission, but the PDF itself remains a public file.

**Signups are captured in HubSpot.** The embedded form on `free-template/index.html` submits to HubSpot and only redirects to the download page if HubSpot accepts it. The page itself still isn't a true gate, since the PDF is a public file.

Once real signups are flowing in, consider also removing the direct link to the PDF from search indexing (the page already has `noindex` set, which stops Google from indexing it — but that's not the same as making it inaccessible to someone with the link).

### Linking it up
Right now this page isn't linked from anywhere else on the site — homepage, nav, or blog posts. It exists but won't get discovered until you add a link (a blog post CTA, a homepage banner, or a LinkedIn post pointing straight at `free-template/index.html` all work).




- Everything is inline in one file on purpose — easiest to hand off, easiest to deploy anywhere, nothing to break.
- Fonts (Fraunces, Inter, IBM Plex Mono) load from Google Fonts via `@import` — needs an internet connection to render correctly; fine for a live site, just know it won't render fonts correctly if opened fully offline.
- Fully responsive down to mobile — test the nav and step grid at narrow widths after you deploy.

## The pricing page (`pricing/`)

- `pricing/index.html` — starting ("from") prices for the Voice Check, Foundations, Overhaul, Voice Partner and add-ons, in Canadian dollars plus HST. Its styles are in the "pricing page" section at the end of `style.css`. Every page's nav links to it. Full prices and tiers live in the Housestyle pricing scheme doc, not on the site.
