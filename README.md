# Michianalocal

Directory site for Trust Drive clients across the Michiana region. Static HTML/CSS, no build step, deployed the same way as Trust Drive: GitHub → GitHub Actions → Cloudways.

## Structure

```
index.html                  Homepage
business-template.html      Master template — copy this for every new business
categories/
  home-services.html        Example category listing page (duplicate per category)
businesses/                 Live business pages go here (empty for now)
assets/
  logo.png                  Full logo (ML mark + wordmark, vertical lockup)
  mark.png                  Icon-only ML mark (favicon, badges)
css/style.css               Shared stylesheet for every page
.github/workflows/deploy.yml
```

## Adding a new business (once they sign for Trust Drive)

1. Copy `business-template.html` into `businesses/[business-slug].html`.
2. Replace every `[BRACKETED]` value — including inside the two `<script type="application/ld+json">` blocks at the top. These power the SEO/GEO/AEO schema; don't skip them.
3. Paste the business's **ReviewSpark** embed code into the `<!-- REVIEWSPARK_EMBED_CODE_HERE -->` placeholder under `#reviews`.
4. Get the business's Google Maps embed URL (Google Maps → their listing → Share → Embed a map → copy the `src`) and drop it into the `iframe` in `.map-embed`.
5. Add a card for the business to its category page (see `categories/home-services.html` for the pattern) and to the "Newest listings" section of `index.html`.
6. Keep the NAP (name, address, phone) on the page **character-for-character identical** to their Google Business Profile. Mismatches hurt local ranking.

## Adding a new category

Duplicate `categories/home-services.html`, update the title/description/breadcrumb, and add a tile for it to the `.cat-grid` on `index.html`.

## Instagram feed

The homepage embeds a feed via [SnapWidget](https://snapwidget.com) (free tier, no Instagram API approval needed — Instagram's own embed API requires a review process that isn't worth it for a simple feed). Create a widget there for the `@michianalocal` account and swap the placeholder `src` in `index.html`'s `.ig-embed-frame` for the real widget URL.

## Deploy

Same pattern as `fmadmin2015/Trust-Drive-Landing-Page`: push to `main`, GitHub Actions rsyncs the whole folder to Cloudways over SSH. The workflow expects four repo Secrets — `CLOUDWAYS_SSH_PRIVATE_KEY`, `CLOUDWAYS_SSH_USER`, `CLOUDWAYS_SSH_HOST`, `CLOUDWAYS_APP_PATH` — set these on the new repo before the first push.

## Still open

- Real category list/count — the seven categories on the homepage are a starting proposal, not final.
- First business page isn't built yet since there's no client content to put in it — once you have your first Trust Drive signee, send me their info and I'll build the real page from the template.
- `business-template.html`'s inner sections (hero, trust rail, FAQ, etc.) still use the original unstyled markup — only the header/footer share the homepage's design system so far.
