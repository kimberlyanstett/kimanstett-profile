# Kim Anstett — Personal Site

A static personal site built for editorial polish, fast page loads,
and simple maintenance. No build step required.

## Stack

- **HTML5** (semantic, hand-written — no framework overhead)
- **CSS3** (custom design system, no Tailwind or Bootstrap)
- **JavaScript** (~20 lines total — mobile nav toggle + auto-year)
- **Google Fonts** — Fraunces (serif) + Inter (sans)
- **Zero build step** — deploy the folder directly

## File structure

```
kimanstett-site/
├── index.html           # Home page
├── about.html           # About / professional bio
├── experience.html      # Executive experience detail
├── board.html           # Board experience & governance philosophy
├── insights.html        # Recognition, media, community, writing
├── contact.html         # Contact & what you're open to
├── css/
│   └── style.css        # Complete stylesheet
├── js/
│   └── main.js          # Nav toggle + year update
└── README.md            # This file
```

## Design system

- **Typography:** Fraunces (headers, editorial serif) + Inter (body, UI)
- **Palette:**
  - Ink: `#0F1B2D` (deep navy)
  - Ink-soft: `#364559` (secondary text)
  - Bg: `#FBFAF7` (warm ivory)
  - Bg-alt: `#F4F1EA` (alternating sections)
  - Accent: `#8A6D2A` (muted gold — used sparingly)
- **Spacing:** 8px grid, `--space-1` through `--space-8` tokens

All design tokens live at the top of `css/style.css` in `:root`.
Change one variable, restyle the whole site.

## Editing content

**All content is in the HTML files directly.** No CMS, no build step,
no Markdown pipeline.

To add a new role:
1. Open `experience.html`
2. Copy the pattern of an existing `<article class="experience-item">`
3. Update the company, role, tenure, scope, summary, and bullet list
4. Add the `id="companyname"` if you want to link to it from the home page

To add a new board seat:
1. Open `board.html`
2. Same pattern as above

To publish a new insight or article:
1. Open `insights.html`
2. Add a new section under "Writing"
3. (Later, if you want a full blog, create a `posts/` folder and one
   HTML file per post — no framework needed)

## Local preview

Just open `index.html` in a browser. Or serve locally:

```bash
# Python
python3 -m http.server 8000

# Node
npx serve .

# Or just double-click index.html
```

Then visit `http://localhost:8000`.

## Deployment options

### Option 1 — Cloudflare Pages (recommended)

**Cost:** Free. Bandwidth is unlimited. HTTPS is automatic.

1. Create a public GitHub repo and push this folder to it
2. Sign in to [Cloudflare Pages](https://pages.cloudflare.com)
3. "Create a project" → connect to your GitHub account → select the repo
4. Framework preset: `None`
5. Build command: leave blank
6. Build output directory: `/` (or the folder name if you nested it)
7. Deploy

Custom domain: In the project settings, add your domain (e.g. `kimanstett.com`).
Cloudflare will guide you through DNS records if the domain is registered
with them (recommended — buy the domain at Cloudflare Registrar for wholesale
pricing) or provide instructions for another registrar.

**Auto-deploy:** every `git push` to `main` deploys automatically in under
a minute.

### Option 2 — Netlify

**Cost:** Free tier is generous (100 GB bandwidth/mo).

1. Push to GitHub as above
2. Sign in to [Netlify](https://app.netlify.com)
3. "Add new site" → import from Git
4. Build command: leave blank
5. Publish directory: `/` (or the folder name)
6. Deploy

Add a custom domain in site settings.

### Option 3 — GitHub Pages

**Cost:** Free.

1. Push to a repo named `<username>.github.io`
2. In repo settings → Pages → Branch: `main`, folder: `/ (root)`
3. Site is live at `https://<username>.github.io`

Custom domain via a `CNAME` file if you want `kimanstett.com`.

### Option 4 — Any static host

The whole site is plain HTML/CSS/JS. It'll run on:
- AWS S3 + CloudFront
- Vercel
- Render
- Firebase Hosting
- A basic web server on your own hardware

## Domain recommendation

Buy `kimanstett.com` (or `.io`, or `.co`) through
[Cloudflare Registrar](https://www.cloudflare.com/products/registrar/).
They sell domains at wholesale cost with no markup and no upselling.
Point it at Cloudflare Pages via their dashboard — one click.

## Analytics recommendation

Add [Cloudflare Web Analytics](https://www.cloudflare.com/web-analytics/)
(free, privacy-first, no cookie banner needed) or
[Plausible](https://plausible.io) ($9/mo, similarly privacy-first).

Skip Google Analytics — it's overkill for a personal site and adds a
privacy-notice requirement.

## Migration path to Astro or Next.js

If the site outgrows plain HTML — for example, if you start publishing
weekly and want a proper blog with tags, RSS, and reading time
estimates — the port to Astro is straightforward:

1. `npm create astro@latest`
2. Copy the CSS into `src/styles/global.css`
3. Convert each HTML page into an `.astro` file — the JSX-like syntax
   maps 1:1 with your current HTML
4. Move the nav and footer into `<Layout>` components
5. Content pages become Markdown in `src/content/`

The design and information architecture we've built here transfer
cleanly. No rework needed.

## Maintenance notes

- **Update the year:** handled automatically by `main.js`
- **Update recognition/awards:** edit `insights.html` and `index.html`
- **Add a new role:** edit `experience.html` and add a card in `index.html`
- **Update the CTA copy:** search for "Currently open to conversations" in
  `index.html`, `experience.html`, `contact.html`
- **Change the palette:** edit CSS variables in `:root` at the top of `style.css`

## Accessibility

- Semantic HTML5 (`<nav>`, `<section>`, `<article>`, `<footer>`)
- Sufficient color contrast (WCAG AA)
- Keyboard-navigable
- No JS required to read content (progressive enhancement)
- Skip-to-content pattern can be added if desired

## Performance

- Zero JavaScript frameworks
- Two web fonts (Fraunces + Inter) loaded via Google Fonts with preconnect
- No images (yet) — add optimized WebP if you add photography later
- Expected Lighthouse scores: 100/100/100/100

## What's not built yet (deliberately)

- **Blog / posts folder** — add when you actually have 3+ pieces to publish
- **Photography** — a professional headshot is worth adding; ask a photographer
  for a landscape crop suitable for the hero section
- **Contact form** — currently uses `mailto:` link, which is fine. If you
  want a form, use Netlify Forms or Cloudflare Turnstile — no backend needed
- **Media kit / press page** — worth adding when you have a photographer's
  headshot and a short-bio + long-bio + fact-sheet package to distribute
- **Downloadable resume PDF** — worth adding; export from Word/Docs, place
  in the site root, link from experience page and contact page
