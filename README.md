# pflugervillewatersoftener

Rank-and-rent local lead-generation site for water softener services in
Pflugerville, TX (`pflugervillewatersoftener.com`). Built with Astro (static
output). Deployed via Vercel on push to `main`.

Cloned from the `water-softener-boilerplate` template — see that repo's
`PROVISION.md` for how sites like this one get created.

Repo: https://github.com/assignmenthelptalk/pflugerville

## Status

| Item | State |
|------|-------|
| Site built from boilerplate (23 pages, 0 build errors/warnings) | Done |
| City data in `site.config.ts` (sourced, see below) | Done |
| Local content (water quality, hard water, FAQ) | Done |
| Homepage neighbourhood map | Done |
| Logo, favicon, branded images | Done |
| Content quality gate (PROVISION.md Step 6b) | Not run |
| Vercel project and domain (Steps 7-8) | Not done |
| Google Search Console and citations (Steps 9-10) | Not done |
| Tenant phone, email, address, About-page facts | Placeholders until a tenant signs |

## City data and sources

All city data lives in `src/site.config.ts` — no CMS layer. To update any
detail after a tenant signs, edit the fields directly and `git push`; Vercel
rebuilds and redeploys automatically.

- **Hardness: 9-10 GPG, "Hard".** Source: City of Pflugerville 2024 Consumer
  Confidence Report. Highest reported calcium 40.3 ppm and magnesium 16.4 ppm
  give about 168 mg/L total hardness (2.497 x Ca + 4.118 x Mg), roughly 9.8
  GPG. A third-party source lists 177.5 mg/L (10.4 GPG). The 14-17 GPG figure
  in the boilerplate's target-cities table was not supported by the utility
  report and was replaced.
- **Water source:** Lake Pflugerville surface water (pumped from the Colorado
  River, originating in the Highland Lakes) plus Edwards Aquifer groundwater.
- **Authority:** City of Pflugerville Public Utilities.
- **County / population:** Travis County, 65,191 (2020 Census).

### Still to verify

- ZIP code `78728` (78660 and 78691 are Pflugerville ZIPs).
- Neighbourhood names against Zillow, Realtor.com, or the city site (PROVISION.md
  Step 5c checklist). Map pin coordinates come from OpenStreetMap.

## Content

22 pages read from the config, plus a QDP-gated `[serviceArea]` dynamic route
(see PROVISION.md Step 5c). No service areas are provisioned yet.

Pflugerville-specific additions on top of the boilerplate:

- `water-quality`: table of the report's 2024 mineral readings and a "where
  the water comes from" section.
- `hard-water`: "Why Pflugerville water is hard" section.
- `faq`: three Pflugerville-specific questions.

## Map

`src/components/PflugervilleMap.astro` (Leaflet, OpenStreetMap tiles with a CSS
inversion filter — do not switch to CARTO or Stadia, see CLAUDE.md). The map is
static: no zoom controls, no scroll/touch zoom, no panning. It frames itself
once around the neighbourhood pins on load and the first neighbourhood
(Falcon Pointe) is preselected so the report panel is never empty.

## Logo, favicon, and images

- `public/logo.svg`: full lockup (ring emblem plus "PFLUGERVILLE / WATER /
  SOFTENER").
- `public/favicon.svg`: the ring emblem alone. The site header uses the same
  emblem inline with the business name from the config.
- `src/assets/images/`: 25 WebP images (1408x768) wired into the homepage,
  17 page headers, and the About page. Each carries a semi-transparent logo
  badge baked into one corner.
- `brand_assets/unbranded-images/`: the originals without the badge.
- `scripts/brand_images.py`: re-applies the badge. Run it after replacing an
  original (the docstring explains the logo render input). `BADGE_OPACITY` sets
  the transparency.
- `brand_assets/unused-images/`: five generated images that show New Mexico
  adobe homes and don't fit Pflugerville. Not part of the site.
- `IMAGE-PROMPTS.md`: the generation prompts. Neighbourhood, new-construction,
  contact, and the About page header have no image yet and show the hardness
  stat card instead.

## Development

```
npm install
npm run dev      # local dev server
npm run build    # astro check && astro build — must complete with 0 errors, 0 warnings
```
