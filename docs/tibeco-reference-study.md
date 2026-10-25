# TIBECO Group as the design reference — the study

Management asked for the Lusail Corp site to be designed like TIBECO Group's
(<https://www.tibecogroup.com/>), and for TIBECO's **platforms** to become
Lusail's **sectors**. This note records what was studied, how the two sites
map onto each other, what was built, and what still needs the Group's eye.

## What was studied

The reference's own source, the `tibeco-9a2c97f1` repository on the Group's
GitHub (a React site built with Tailwind; the live site is deployed from it).
Every component, page and design token below was read from that source, not
inferred.

### TIBECO's site, as its source describes it

| | TIBECO Group |
|---|---|
| **Grounds** | Dark throughout: page `hsl(220 20% 10%)`, card `hsl(220 18% 14%)`, "mannai-dark" band `hsl(220 25% 8%)`, secondary `hsl(220 15% 20%)`, border `hsl(220 15% 22%)`. Type near-white; muted copy `hsl(215 20% 65%)`. |
| **Accent** | One amber gold, `hsl(38 90% 55%)`, for labels, rules, pins, the primary button. |
| **Type** | Playfair Display (400–700) for every heading; Raleway (300–700) for everything else. Labels uppercase, tracked `.2em`–`.3em`. |
| **Shapes** | `--radius: 0.25rem`; cards `rounded-lg` (8px) with a hairline border that turns `accent/40` on hover. No shadows on cards. |
| **Bar** | Fixed, transparent; `bg-mannai-dark/95` + blur + shadow after 50px of scroll. Left: "☰ Platforms". Centre: the logo (280×80; the monogram alone under 640px). Right: "Corporate ☰". |
| **Menus** | Two drawers over a dimmed page. Left (Platforms): the three platforms, each expanding to its five areas, with icon, uppercase name and Arabic. Right (Corporate): Home, Who We Are, Careers, Supplier Portal, Contact; a profile-PDF button; LinkedIn. |
| **Home** | Preloader (three bouncing dots, 1.8s) → full-screen hero: six photographs crossfading every 5s, `mannai-dark/60` veil, a faint 500px circle, centred "TIBECO GROUP" / "Commerce \| Investment \| Services" / "ELITE INTERNATIONAL BUSINESS GROUP" in gold, two joined buttons ("Learn More" \| "Our Platforms"), slide dots → **Corporate Statement** (image, two paragraphs, "DISCOVER TIBECO") beside **Why TIBECO GROUP** and an **Institutional Strength** box → **Core Business Platforms**: each platform a header row (icon, uppercase name, Arabic, hairline, one line) over a 4-column grid of 4:3 image tiles, the name revealed on hover → **Global Presence**: centred heading with Arabic above and a gold rule, a Mercator map with pulsing pins and dashed gold lines, a paragraph and two figures → Partners marquee → Certificates marquee. |
| **Platform page** | PlatformHero (full-screen centred, with a pill badge "TIBECO – Commerce Platform"; or left-aligned 80vh, split, compact 60vh) → sticky tabs (gold fill on the active one) → sections alternating card and page grounds: a 3-column "Strategic Positioning" (heading + rule + gold label, two paragraphs), icon-card grids, a numbered timeline, bullet lists, a two-card "Platform Integration", a centred **closing statement**, the **Supplier Portal band**. |
| **Who We Are** | 60vh photograph, "TIBECO GROUP" and the section tabs in the hero; Chairman's message, Who We Are, Vision, Market Positioning, Strategic Philosophy, Credentials — each a heading, Arabic, a 64px gold rule, and columns of small muted paragraphs; photographic dividers between. |
| **Footer** | One line: the logo at the left; © · Privacy Policy · Terms · Supplier Portal · Contact Us at the right. |
| **Corner** | A 40px square mail button opening a small contact card; a back-to-top button above it after 400px. |
| **Supplier Portal** | A portal strip under the bar (Supplier Portal · بوابة الموردين · Opportunities · How it works · Requirements · Register); the home with "Supply the Group. Bid in one place.", a "Closing soon" card, how it works as four numbered cards, categories, the opportunities table, requirements and principles, fraud notice and support. Already carried over to this site in an earlier pass. |
| **Arabic** | Every section heading carries an Arabic sub-label in the accent; platforms and areas carry Arabic names. |

## Mannai Corporation, the reference behind the reference

Management also pointed at <https://mannai.com/>. It could not be opened from
the build environment (the network policy refuses the host), but two things
are known about it with confidence:

1. **TIBECO's site is built on Mannai's.** TIBECO's source names its colour
   tokens `mannai-dark`, `mannai-navy` and `mannai-gold`, and carries
   redirects for the Mannai activities it started from (`/activities/*`,
   `/platforms/automotive`, `jewellery`, `travel`, `logistics`, `geo`,
   `retail`, `facility`). So the grammar carried into this site — the dark
   grounds, the gold, the fixed bar with two menus and the mark in the
   middle, the activities grid, the executive team and news pages — is
   Mannai's grammar as TIBECO adopted it.
2. **Mannai's structure, from its search-index listing:** the homepage says
   the Corporation "is broadly divided into two key activities, Trade and
   Services"; a "What We Do" section lists its activities (Mannai
   Technologies, Automotive, Jewellery, Energy & Industrial Markets,
   Geological and Material Testing, Travel, Logistics, Engineering), each at
   `/activities/<slug>/`; divisions sit under activities (Automotive has a
   passenger-vehicle division and a heavy-equipment division; ICT has Mannai
   Networks, InfoTech and TechHub); and the corporate pages are Executive
   Team, News and Contact.

What was taken from it here: **an activity opens to the divisions under it.**
That is the request "a sector we can open and see the companies under it",
and it is built twice — in the Sectors drawer, where each sector expands to
its overview and its companies, and in the **sector explorer** on the home
page and the sectors index, where the open sector shows its photograph, its
line, its companies and its business areas.

## How TIBECO's structure maps onto Lusail Corp

| TIBECO Group | Lusail Corp | Where |
|---|---|---|
| "ELITE INTERNATIONAL BUSINESS GROUP" | "DIVERSIFIED QATARI BUSINESS GROUP" | `SITE.descriptor` |
| "Commerce \| Investment \| Services" | "Investment \| Trade \| Supply \| Services" | `SITE.fields` |
| **Three platforms** — Commerce, Investments, Services | **Seven sectors** | `SECTORS` |
| "☰ Platforms" drawer: a platform expands to its areas | "☰ Sectors" drawer: a sector expands to its overview and its companies | `header()` |
| "Corporate ☰" drawer: Home, Who We Are, Careers, Supplier Portal, Contact, profile PDF, LinkedIn | "Corporate ☰" drawer: Home, About Us, Work With Us, Supplier Portal, Contact, the Contact button, LinkedIn when set | `CORPORATE` |
| Core Business Platforms: header row + 4-column image tiles per platform | Core Business Sectors: the sector explorer (open a sector, see its companies and areas); Group Companies: five tiles | `sectorExplorer()`, `companyTiles()` |
| A page per platform (× 5 areas = 15 pages) | A page per sector (7), each listing its business areas | `pageSector()` |
| Business areas on a platform page | Business areas on a sector page — each a product or service of a company in the sector, tagged with `in: [...]` | `areasOf()` |
| Corporate Statement / Why TIBECO / Institutional Strength | The same three blocks, from the Group's own copy | `pageHome()` |
| Global Presence map + 2 figures | The sourcing globe + the Group's 4 figures (counted from the content) | `reachGlobe()`, `FIGURES` |
| Certificates and Partners marquees | Left out — the Group has none to show yet | — |
| Preloader | Left out — an artificial 1.8s delay | — |
| Who We Are with tabs | About Us (the Group, vision and mission, values, value creation, how we work) | `pageAbout()` |
| Careers | Left out — no careers page by the Group's earlier decision | — |

Seven top-level sectors do not fit a bar, which is also why TIBECO puts its
platforms behind a drawer: the structure carries over unchanged. Three of the
seven sectors are worked only through TIBECO Group today; their pages say so
("through TIBECO Group") and link to tibecogroup.com.

## Reference, not copy — where the site is deliberately its own

The second pass matched TIBECO closely; management asked for the reference
to be used, not copied. These are the places the site now departs from it
on purpose:

| TIBECO | Lusail Corp |
|---|---|
| The home opens on the group's name, centred, in a faint ring, over "ELITE INTERNATIONAL BUSINESS GROUP" | The home opens on the Group's own statement, "Building Businesses. Creating Value.", left-aligned, with the descriptor as a small line and the photographs **named along the foot** — the Group, then five of its fields |
| "Corporate Statement" / "Why TIBECO GROUP" / "Institutional Strength" | "The Group" / "What makes it a group" — the Group's four claims as a numbered list, in its own words |
| "Core Business Platforms": a header row and image tiles per platform | **The sector explorer**: open a sector, see its photograph, line, companies and business areas — a component TIBECO does not have |
| A platform page opens full-screen and centred, with a pill badge | A sector page opens like a company page: crumb, "Sector 02 of 07", name, Arabic, line, two buttons, and a **facts bar** along the foot — one grammar for every entity page on the site |
| A one-line footer | The mark and the Group's line, then Sectors, The Group and Reach us as three columns, then the legal line |
| "Corporate" | "The Group" — the Group's own word for itself |
| Two asks at the foot of the home (the portal band, then the footer) | One closing band with both routes: enquiry, or the Supplier Portal |
| Preloader, partners and certificates marquees | Left out: nothing to show yet, and an artificial delay is not a feature |

## The design review, and what it changed

With the site built, every page was screenshotted at 1440 and 390 — full
page, first screen and the interactive states — and reviewed as a designer
would. The verdict: a coherent system that clears the reference on
structure, with second-order faults repeated across pages. What changed:

- **One button hierarchy.** Wherever two actions stood together, the first
  is gold and the second a gold-tinted outline. The dark-grey filled button,
  which read as disabled on these grounds, is gone.
- **One accent.** ROMA's green, Cavallo's steel blue and Nero's tan made five
  companies look like four templates; every company is gold now. The
  colours stay recorded in `data/site.js`, unrendered.
- **Grids sized to what they hold.** A sector with one business area shows
  it as a wide feature card; two show as two halves; a single company fills
  the row with its photograph beside its name — not one card and three empty
  columns.
- **Photographs shot on white** are darkened and washed at the foot so they
  sit in the canvas.
- **A top scrim on every photographic opening**, so the bar's lettering never
  sits on a bright sky; split openings start their photograph under the bar.
- **The phone**: the corner button is smaller, waits until the page has
  moved, and hides while a drawer is open; the company tiles run one to a
  row with the name alone; business areas run two to a row, which halves
  the longest page; the footer's links sit in two columns; the two burgers
  are labelled; the sector tabs fade at the edge and snap.
- **Copy**: the forms' footnote said "to run the event" everywhere; it now
  says what each form is for. The sector closing line and company quotes are
  set left with a gold rule, at a reading measure.
- **Headings** are all sentence-case Playfair with a small gold eyebrow;
  the two tracked-uppercase ones are gone.
- **The Group drawer** carries the five companies, so its middle is not
  empty; the drawers are 360px so a sector name holds one line; the
  slideshow tabs fill in gold over the five seconds a photograph stands.

What the review asked for that needs the Group: its own photography
(TODO, item 0).

## What was kept Lusail's

- **The gold** is the logo's `#D3A750`, not TIBECO's amber `hsl(38 90% 55%)`.
  On these grounds it reads at 9:1, so it is text as well as mark. One token.
- **The globe** stays in place of TIBECO's flat map: it already shows the
  Group's sourcing as gold arcs into Doha, in the same language.
- **The content** is the Group's own throughout; nothing of TIBECO's copy
  was carried over.

## The new site, page by page

```
/                          Home
/about/                    The Group
/sectors/                  The seven sectors, as tiles
/sectors/<slug>/           One sector — the platform page, re-cast
/companies/<slug>/         One company (TIBECO opens tibecogroup.com instead)
/partnerships/             Work With Us
/supplier-portal/          The Supplier Portal, /opportunities/, /register/, /code/
/contact/                  Channels and the enquiry form
```

## What to confirm with the Group

- **The Arabic sub-labels** under section headings and sector names were
  written for this redesign (`AR` in `build/render.js`, `ar` in
  `data/site.js`). A native reader should check them before launch; they can
  be removed by emptying `AR` and the `ar` fields.
- **The descriptor line** and the fields line under the Group's name.
- **Business-area tags.** Which sector pages each TIBECO and Lusail
  Commercial product appears on (`in: [...]`) is a reading of the products,
  not a statement from the companies.
- **Three sectors through TIBECO alone.** Investments, Energy & Industrial
  and Technology have no Lusail company of their own. Either fold them into
  fewer sectors or add the companies that belong there.
- **The gold.** If management wants the palette to follow TIBECO exactly, set
  `--gold` to `#f4a825`.
