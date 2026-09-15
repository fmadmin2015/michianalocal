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

The homepage embeds a live feed via [SociableKIT](https://sociablekit.com) (free tier — 1 widget, 2,000 views/month, manual sync, small watermark — no Instagram API approval needed), wired up for the `@michianalocal` account. To swap the widget (new account, layout change, etc.), create a new one at sociablekit.com, grab its embed link (Embed on Website > Website > Link), and replace the `src` in `index.html`'s `.ig-embed-frame`.

## Deploy

Same pattern as `fmadmin2015/Trust-Drive-Landing-Page`: push to `main`, GitHub Actions rsyncs the whole folder to Cloudways over SSH. The workflow expects four repo Secrets — `CLOUDWAYS_SSH_PRIVATE_KEY`, `CLOUDWAYS_SSH_USER`, `CLOUDWAYS_SSH_HOST`, `CLOUDWAYS_APP_PATH` — set these on the new repo before the first push.

## Still open

- Real category list/count — the seven categories on the homepage are a starting proposal, not final. Only `categories/home-services.html` exists so far.
- HS Construction (`businesses/hsconstructiongroup.html`) is the first live business page. It's a service-area business with no public street address, so its NAP card shows service area instead of an address and skips the Google Maps embed — most future businesses will have a real address to fill in instead.
