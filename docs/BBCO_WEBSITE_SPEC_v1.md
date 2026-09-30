# BBCO Website Spec v1

> CODEX: Implement this spec. Do not invent features. Do not add pages. Access model is real downloads + license after cancel + subscription core + $69 one-off packs. Identity: Ink #121212, Paper #F4F1EA, Rule #CBC7BE, Signal #8F2D2A. Wordmark BACKGROUND BRAND CO. Swiss + archive. No DRM. No free trial downloads. Working pack titles are pending clearance — use slugs, not public “pending” labels.

## 0. Build rules for Codex

### Product rule
Background Brand Co. is a downloadable production-asset library, not a browser-only design tool.

Customers browse publicly, authenticate when they need rights/files, and download real production files after an entitlement check. The website records what was downloaded, under which license, and when.

### Locked company and product
- Company: Background Brand Co., LLC.
- Product: Scene-Ready Brand Packs for visual media.
- Launch catalogue: 5 packs only:
  1. Coffee
  2. Water / beverage
  3. Grocery / snack
  4. Restaurant / delivery
  5. Wellness / athletic
- Hero line: **Brands built to live inside other stories.**
- Campaign platform: **You’ve seen it before. You just haven’t.**
- First customers: production designers, art directors, creative directors, agencies, commercial/content studios.
- Digital library first.
- No physical props, contributor marketplace, or public API in MVP.

### Locked access + money model
1. Customers download production files. That is the product.
2. After cancel they still possess files. Creator/Pro: finished work already published while subscribed stays covered, but no new use after the paid term ends, subject to final counsel language. Studio: organization may continue using already downloaded packs for new projects according to the Studio agreement.
3. Do not build a browser-only asset vault.
4. One-off pack purchase is allowed. It grants that pack only under the purchased license class.
5. Pricing test:
   - Creator: $29/month
   - Pro: $99/month
   - Studio: custom
   - Single pack: $69
6. No Creative Commons on Scene-Ready Packs.
7. No “$1M indemnification” or “100% human-made” claims.
8. Certificate PDF is generated per qualifying pack/version entitlement and records pack name, licensee, plan, date, permitted channels, certificate ID, and license revision.
9. Raw files may not be redistributed, resold, registered as customer trademarks, or used to train foundation models.
10. Public previews are visible; full ZIP files require auth + valid entitlement.

### Identity
- Primary wordmark: `BACKGROUND BRAND CO.`
- Secondary mark: Shared Spine BB monogram.
- Ink: `#121212`
- Paper: `#F4F1EA`
- Rule: `#CBC7BE`
- Signal: `#8F2D2A`, used sparingly.
- Visual character: quiet Swiss + archive + rights desk.
- Catalogue supplies color; parent UI stays neutral.
- No gradients, film-reel icons, clapperboards, novelty film graphics, fake grain, startup SaaS styling.

## Repo layout

Codex should create this structure when implementation begins:

```text
/apps/web
/apps/api
/packages/entitlements
/packs/_dummy
/docs
```

Recommended responsibility split:

```text
/apps/web
  public site
  auth screens
  account/download history
  checkout entry points

/apps/api
  Stripe webhook handling
  entitlement checks
  signed download URL generation
  certificate generation / verification

/packages/entitlements
  entitlement evaluation
  plan/channel constants
  shared types
  idempotent grant/expire helpers

/packs/_dummy
  BBCO-DUMMY-CAFE-v0.1
  manifest.json
  test files

/docs
  BBCO_WEBSITE_SPEC_v1.md
  BBCO_CODEX_BUILD.md
```

## Out of scope

Do not build:
- physical shop
- physical prop manufacturing
- 200-brand catalogue
- contributor uploads
- public API
- community forum
- team seat admin
- DRM
- browser-only asset editor
- blog farm
- fake testimonials
- founder essays
- AI-generation playground
- public “pending clearance” labels
- enterprise procurement system
- marketplace contributor tools
- complex Studio self-serve contracting

---

## A. Product logic

### Entitlement matrix

| Capability | Guest | Creator $29 | Pro $99 | Studio | One-off |
|---|---:|---:|---:|---:|---:|
| Browse packs | Yes | Yes | Yes | Yes | Yes |
| View watermarked previews | Yes | Yes | Yes | Yes | Yes |
| View complete asset manifest | Yes | Yes | Yes | Yes | Yes |
| Download eligible packs | No | Yes | Yes | Yes | Purchased pack only |
| Print assets onto props | No | Yes | Yes | Yes | Yes |
| Generate license certificate | No | Yes | Yes | Yes | Purchased pack |
| Personal / indie digital | — | Yes | Yes | Yes | Yes |
| Client commercial work | — | Limited / No | Yes | Yes | Yes |
| Paid web/social ads | — | Limited / No | Yes | Yes | Yes |
| Major film / TV / OTT / broadcast | — | No | No | Yes | Studio or add-on |
| Multiple seats | — | No | No | Yes | No |
| New projects after cancellation | — | No | No | Per Studio agreement | Yes within purchased scope |
| Previously published finished work remains licensed | — | Yes | Yes | Yes | Yes |

### Trial
Decision: **no free downloadable trial at launch.**

Guests can inspect:
- watermarked scene previews
- exact asset lists
- file formats
- dimensions
- licensing summary

A free sample mini-pack may be tested later only if conversion data supports it.

### Why we allow downloads
Art departments need:
- vectors
- PDFs
- print-ready packaging
- textures
- offline files
- source assets

The value proposition is:

**Download. Print. Place. Shoot.**

Trying to prevent customers from possessing files would break the core use case.

### One-off vs subscription decision tree

**Need one brand for one job?**  
Buy one pack.

**Need two or more brands, ongoing work, or multiple projects?**  
Subscribe.

**Need TV, film, streaming, broadcast, multiple seats, or organizational rights?**  
Studio.

### One-off pricing
Test price: **$69 per pack**.

This is approximately 2.4× the Creator monthly price, preserving subscription as the default.

Do not use “lifetime ownership.” Use:

**Perpetual production license for this pack under the purchased license scope.**

---

## B. Sitemap

### Primary navigation
- Brands
- Scenes
- Pricing
- License
- Custom
- Log In
- Primary CTA: **Browse Library**

### Public URLs

```text
/
 /brands
 /brands/[slug]
 /scenes
 /scenes/[slug]
 /pricing
 /license
 /custom
 /about
 /login
 /signup
 /checkout
 /legal/terms
 /legal/privacy
 /legal/production-license
```

### Logged-in URLs

```text
/account
/account/downloads
/account/certificates
/account/billing
/account/profile
```

### Footer

**Library**
- Browse Brands
- Browse by Scene
- Pricing

**Rights**
- License
- Terms
- Privacy

**Company**
- About
- Custom Brand Studio
- Contact

Footer metadata:

`© Background Brand Co. · BBCO`

Keep the footer institutional and quiet.

---

## C. Pages

# Home `/`

### Purpose
Explain the product in seconds and move a professional toward the library.

### Module 1 — Hero

**Headline**  
# Brands built to live inside other stories.

**Subhead**  
Production-ready fictional brands for props, sets and visual media. Download the files. Print what you need. Put them on camera.

**Primary CTA**  
Browse the Library

**Secondary CTA**  
See How Licensing Works

**Hero scene**  
One believable production environment containing a coherent fictional brand system. Do not overload the hero with unrelated catalogue brands.

**Small annotation**  
None of these brands exist.

### Module 2 — Campaign statement

# YOU’VE SEEN IT BEFORE.  
# YOU JUST HAVEN’T.

Real worlds are full of brands. Fictional worlds should feel the same.

### Module 3 — Five launch packs

Five tiles:
- Coffee
- Water / Beverage
- Grocery / Snack
- Restaurant / Delivery
- Wellness / Athletic

Each tile shows:
- hero scene
- pack category
- asset count
- starting entitlement
- View Pack

No unnecessary carousel interaction.

### Module 4 — How it works

**01. Choose a world**  
Find the brand that fits your scene.

**02. Download the production files**  
Vectors, PDFs, transparent graphics, mockups and application notes.

**03. Print. Place. Shoot.**  
Use the assets inside eligible finished productions.

### Module 5 — Browse by scene

Tiles:
- Café
- Dorm
- Office
- Kitchen
- Grocery
- Gym
- Restaurant
- Street / Exterior

CTA: **Browse All Scenes**

### Module 6 — License confidence

**Headline**  
Built for art departments. Documented for production.

**Clear usage rights**  
Know what your plan covers.

**License certificates**  
Generate proof for each licensed pack.

**Production-ready files**  
Not just flattened mockups.

CTA: **Read the License**

### Module 7 — Pricing bridge

**Need one pack? Buy one.  
Need a library? Subscribe.**

Creator — $29  
Pro — $99  
Single Pack — $69  
Studio — Contact

CTA: **Compare Plans**

### Module 8 — Launch film slot

16:9 embed slot.

Caption:

**None of these brands exist. Every one was built to belong.**

### Cut from Home
Do not add:
- founder essay
- blog feed
- giant FAQ
- fake testimonials
- fake usage stats
- fake studio logos
- long AI explanation

---

# Browse Brands `/brands`

### Purpose
Fast library discovery.

### Header
# THE LIBRARY

Fictional commercial worlds built for production.

### Filters
- Category
- Scene
- License compatibility
- Newest
- Alphabetical

At launch, keep filtering lightweight because there are only five packs.

### Pack card
- image
- cleared brand name
- category
- asset count
- scene tags
- subscription access / $69 single pack
- View Pack

---

# Browse by Scene `/scenes`

### Purpose
Match the way art departments think.

### Headline
# WHAT ARE YOU DRESSING?

Scene tiles:
- Café
- Dorm
- Kitchen
- Office
- Gym
- Grocery Store
- Restaurant
- Street
- Locker Room
- Apartment

Selecting a scene displays relevant packs and exact assets suited to it.

---

# Brand Pack `/brands/[slug]`

### Module 1 — Hero
Show:
- brand name
- category
- one-sentence fictional positioning
- primary in-scene mockup

CTAs:
- **Download with Subscription**
- **Buy This Pack — $69**

Unauthenticated users route to signup/checkout.

### Module 2 — Scene uses

Example:

**Works naturally in:**  
Café · Office · Dorm · Kitchen · Street

### Module 3 — What’s inside

Structured asset manifest.

Coffee example:
- 3 logo configurations
- hot cup artwork
- cold cup artwork
- sleeve
- 12 oz bag front/back
- 2 lb bag front/back
- napkin
- carrier
- menu board
- storefront sign
- apron mark
- window decal
- transparent logos
- source vectors

Always show the actual quantity.

### Module 4 — File formats

**AI / SVG / PDF / PNG / JPG**

Include:
- CMYK masters
- sRGB previews
- 300 ppi where raster
- documented physical sizing

### Module 5 — Production preview gallery

Show:
- flat artwork
- applied prop
- close-up
- environmental scene
- backside/package details

Public previews may be watermarked.

### Module 6 — License coverage

Small table:
- Creator — indie/personal digital
- Pro — paid commercial/client web/social/photo
- Studio — film, TV, streaming, broadcast

Link: **Compare full rights**

### Module 7 — Fictional brand disclaimer

> This is a fictional production brand. It is licensed for use inside eligible visual productions. It is not a consumer business being offered for sale, and your license does not transfer ownership of the brand identity.

### Module 8 — Technical notes
- dimensions
- printing advice
- recommended blanks/prop sizes
- bleed
- color profile
- application tips

### Module 9 — Version
Show `Pack version 1.0` and changes/additions.

### Module 10 — Related scene packs
Maximum 3.

---

# Pricing `/pricing`

### Hero
# One project or an entire library.

Choose the rights and access that match how you work.

| | Creator | Pro | Studio |
|---|---:|---:|---:|
| Price | $29/mo | $99/mo | Custom |
| User | Individual | Professional / small company | Organization |
| Library downloads | Yes | Yes | Yes |
| Personal content | Yes | Yes | Yes |
| Client commercial | Limited / No | Yes | Yes |
| Paid social / web ads | Limited / No | Yes | Yes |
| TV / broadcast | No | No | Yes |
| Film / OTT | No | No | Yes |
| Seats | 1 | 1 initially | Multi-seat |
| License certificates | Yes | Yes | Yes |
| New use after cancellation | No | No | Per Studio agreement |

### Single-pack block

# Only need one?

**Buy any pack individually from $69.**

Includes ongoing use of that pack within the purchased commercial scope.

Broadcast/film requires Studio or an applicable add-on.

CTA: **Browse Single Packs**

### After-cancel plain English

Creator / Pro:

> Cancel anytime. Finished productions published while your subscription was active remain licensed. You may keep downloaded files for your records, but you may not begin new productions with them after your subscription ends.

Studio:

> Studio agreements can include continued new-project use of packs downloaded during the active agreement. Final terms are defined in the Studio contract.

**COUNSEL:** final wording required.

---

# License `/license`

### Public explainer

> **Use the brand in your production. Don’t become the brand.**
>
> Background Brand Co. licenses fictional brand assets for use inside eligible finished visual works. Depending on your plan, you may print the supplied artwork onto props, resize or adapt it for your scene, and incorporate it into photography, video, advertising and other approved productions.
>
> Your license does not transfer ownership of the fictional brand or the raw files. You may not redistribute or resell source assets, register catalogue names or logos as your trademarks, operate a real-world business under them, build a competing asset library, or use the library to train foundation models.
>
> Standard catalogue brands are non-exclusive.
>
> Creator, Pro and Studio plans cover different customers and distribution channels. Every eligible download can generate a license certificate identifying the pack, licensee, plan and date.
>
> **See Full Production License →**

### Expandable sections
- Who is licensed
- Permitted productions
- Printing props
- Modifications
- AI-assisted production
- Raw-file restrictions
- Trademark restrictions
- Cancellation
- Studio usage

---

# Custom `/custom`

MVP = waitlist / inquiry only.

### Headline
# Need a world that only exists in your production?

Custom Brand Studio creates bespoke fictional commercial systems for productions that need exclusivity, category specificity or a unique visual world.

### Fields
- Name
- Company
- Role
- Project type
- Category needed
- Timeline
- Distribution
- Exclusivity needed?
- Budget range

Do not show fixed pricing in MVP.

---

# About `/about`

> **Background Brand Co. builds fictional commercial worlds for visual production.**
>
> We create coherent, production-ready brand systems that can live naturally inside sets, props, photography and moving image.
>
> The library exists to remove one recurring production problem: having to invent every background brand from scratch.

No founder biography is required in MVP.

---

## D. Account and commerce

### Sign up
1. Email/password or supported auth.
2. Ask:
   - What do you create?
   - Individual or organization?
3. User enters account.
4. No forced subscription before browsing.

**Empty state**  
Your library is empty.  
Browse a pack to start building your production library.

### Subscribe
1. Select pricing plan.
2. Authenticate if needed.
3. Stripe Checkout.
4. Successful payment creates/updates subscription and entitlement through webhooks.
5. Redirect to:

**Your library is ready.**

Buttons:
- Browse Packs
- View Account

### Buy one pack
1. User selects **Buy This Pack — $69**.
2. Choose eligible license class if needed.
3. Sign in/create account.
4. Stripe Checkout.
5. Create entitlement for exact pack/version.
6. Pack becomes downloadable.
7. Certificate generated on first licensed download or purchase, depending implementation.

Success:

**Pack licensed. Ready for production.**

### Download + certificate
1. User clicks Download.
2. Backend authenticates user.
3. Backend checks entitlement.
4. System logs:
   - user
   - organization
   - pack ID
   - version
   - plan
   - timestamp
5. Certificate is created or resolved.
6. Signed expiring URL is returned.
7. ZIP downloads.
8. Certificate remains available separately.

### Cancel Creator / Pro
1. Account → Billing.
2. Cancel subscription.
3. Show warning:

> Your subscription will remain active until [DATE]. Finished works published while covered remain licensed. After that date, you may view your download history and certificates, but you may not begin new productions with previously downloaded subscription assets.

4. Stripe uses period-end cancellation.
5. At paid-term end:
   - browse remains available
   - history remains
   - certificates remain
   - subscription downloads/re-download disabled

Do not imply files disappear from the customer’s computer.

### Upgrade Creator → Pro
- Immediate upgrade.
- Explain: **Pro adds paid client and broader commercial usage.**
- Billing provider handles proration.
- Entitlement plan updates from effective billing change time.

**COUNSEL:** define how upgraded rights apply to prior downloads.

### Upgrade Pro → Studio
CTA: **Talk to Studio Licensing**

MVP:
- inquiry form
- manual agreement
- admin grant after contract

Do not build a self-serve enterprise contract engine.

### Failed payment
Banner:

**Payment issue — library access is at risk.**

During grace:
- account remains available
- certificates remain
- downloads follow configured billing policy

At lapse:
- history remains
- certificates remain
- subscription download entitlement ends

### Team seats
Studio only.

MVP copy:

**Contact your Studio administrator / Background Brand Co.**

No seat-management dashboard yet.

---

## E. Downloads

### Pack format
Each pack is versioned.

Example:

`BBCO-ALDERROW-v1.0.zip`

Pack contains:
- README
- license summary
- vectors
- print-ready files
- transparent PNGs
- mockups
- textures where applicable
- manifest

### `manifest.json`
Include:
- `pack_id`
- `brand_name`
- `version`
- `release_date`
- file list
- checksums
- categories
- scene tags
- formats
- deprecated/replaced assets

### Entitlement data model
Keep rights separate across:
- User
- Organization
- Subscription
- Pack
- PackVersion
- Purchase
- Entitlement
- DownloadEvent
- Certificate

Never infer rights only from “downloaded = true.”

### Protected download flow

**Request → authenticate → entitlement check → log → certificate resolve/create → signed URL → download**

Signed URLs are access control, not DRM.

### Re-download rules

**Active Creator / Pro**  
Yes.

**Cancelled Creator / Pro**  
No new/re-download access after the paid period ends. History + certificates remain.

**Studio**  
Per agreement.

**One-off**  
Re-download of the purchased pack/version is allowed under the purchased entitlement. Major future redesigns may require a new purchase.

**COUNSEL:** define maintenance update vs new major version.

### Public watermark strategy
Watermark:
- high-resolution mockup previews
- downloadable comp images, if offered

Do not over-watermark tiny thumbnails.

Watermark text:

`BACKGROUND BRAND CO. / PREVIEW`

No giant diagonal stock-photo treatment.

### Sprint 1 dummy pack

`BBCO-DUMMY-CAFE-v0.1`

Purpose:
prove:
- checkout
- entitlement
- signed URL
- download logging
- certificate generation
- cancellation preserving history

The dummy pack is not a public launch brand and grants no real production rights.

---

## F. Catalogue

All launch brand names are working titles until cleared.

Never display `pending clearance` publicly once a pack is released. Clearance must be complete before public release.

| Category | Working title | Scene tags | SEO title pattern |
|---|---|---|---|
| Coffee | Alder Row Coffee | café, office, dorm, kitchen, street | `Alder Row Coffee Fictional Production Brand Pack | BBCO` |
| Water / Beverage | Clearhaven | gym, dorm, office, restaurant, convenience | `Clearhaven Beverage Fictional Production Brand Pack | BBCO` |
| Grocery / Snack | Goodfield Foods | kitchen, grocery, dorm, break room | `Goodfield Foods Fictional Grocery Brand Pack | BBCO` |
| Restaurant / Delivery | Sidecar Kitchen | apartment, office, restaurant, lobby, car | `Sidecar Kitchen Fictional Restaurant Brand Pack | BBCO` |
| Wellness / Athletic | Formline | gym, locker room, training facility, dorm | `Formline Fictional Athletic Brand Pack | BBCO` |

### Required pack-page fields
- Brand name
- Internal clearance status
- Category
- One-line fictional story
- Hero scene
- Asset count
- File formats
- Pack version
- Scene tags
- Physical applications
- Technical dimensions
- Plan compatibility
- Single-pack price
- Related packs
- Production notes
- Preview gallery
- License disclaimer

---

## G. Legal surface

### Fictional brand disclaimer

> This identity is a fictional production asset. It is not presented as an operating consumer business or endorsement by a real company.

### AI-assisted / human-art-directed sentence

> AI may assist our development process. Every library pack is human-art-directed and production-reviewed. Background Brand Co. owns or has sufficient rights to distribute the assets provided, and customer use is governed by the applicable license.

### Trademark restriction

> Your license does not authorize you to register a catalogue brand, name or logo as your trademark or use it as the source identifier of a real-world business.

### Raw-file restriction

> Production use is permitted within your license. Redistribution, resale or sublicensing of raw source assets is not.

### Counsel-required clauses
The final legal package must define:
- named licensee
- seat rules
- permitted distribution
- finished-work definition
- raw-asset definition
- modification rights
- subscription expiration
- one-off ongoing-use scope
- Studio post-term reuse
- prohibited trademark registration
- AI/video incorporation
- model-training prohibition
- warranties
- limitation of liability
- governing law
- termination
- refund language
- DMCA/copyright complaints
- third-party claims
- audit rights if any
- digital-product tax treatment

Do not invent indemnification promises.

---

## H. Analytics

Track events that reveal product-market fit.

### Events

`account_created`

`pricing_viewed`

`plan_selected`
- creator
- pro
- studio

`pack_viewed`
- pack_id
- category
- source

`scene_filter_used`
- scene

`single_pack_checkout_started`

`single_pack_purchased`

`subscription_started`

`first_download`

`pack_downloaded`
- pack
- version
- license class

`certificate_generated`

`subscription_cancelled`
- tenure
- pack_download_count

`studio_inquiry_submitted`

### Primary metrics
- visitor → account conversion
- account → paid conversion
- paid → first download
- downloads per paid account
- one-off → subscription conversion
- Creator → Pro upgrades
- cancellation rate
- percentage of testers who actually use an asset in production

Ignore as standalone KPIs:
- raw pageviews
- follower counts
- vanity engagement
- time-on-page worship

---

## I. MVP sequence

### Week 1 — Commerce skeleton
Build:
- auth
- Stripe Creator subscription
- Stripe Pro subscription
- $69 one-off test purchase
- core data model
- entitlement service
- dummy pack
- private storage
- signed download
- download event
- certificate record

**Goal:** a customer can pay and obtain a valid entitlement.

### Week 2 — Library
Build:
- Brands index
- Pack page
- scene taxonomy
- preview assets
- manifest support
- secure ZIP storage
- download logging

**Goal:** a Pro user can pay, download a real/test pack, and see the download recorded.

### Week 3 — Licensing infrastructure
Build:
- certificate PDF
- certificate verification
- account history
- downloads page
- cancellation behavior
- entitlement expiry
- one-off entitlement persistence
- License page

**Goal:** a customer can hand a BBCO certificate to a producer.

### Week 4 — Identity + conversion
Apply locked BBCO identity.

Build:
- polished Home
- Scenes
- About
- Custom inquiry
- responsive states
- receipts/onboarding
- analytics

**Goal:** product works first; polish comes second.

### Week 5 — Closed beta
Invite 20–50 working professionals.

Observe:
- discovery
- checkout
- print/application
- certificate usefulness
- license confusion
- actual scene use

Fix critical issues before public launch.

---

## J. Implementer prompts

### Web/UI implementer

> Build the Background Brand Co. MVP from the approved site specification and locked identity. Prioritize professional utility, information hierarchy and library discovery. The visual system is film archive + type foundry + rights desk: Ink #121212, Paper #F4F1EA, Rule #CBC7BE, Archive Red #8F2D2A used sparingly. The catalogue provides color; the parent UI stays neutral. Do not introduce decorative film icons, gradients, startup SaaS styling or excessive motion. Build responsive Home, Brands, Scenes, Pack, Pricing, License, Custom, About and Account surfaces.

### Stripe implementer

> Implement Creator $29/month and Pro $99/month recurring subscriptions plus $69 single-pack purchases. Stripe controls payment state; our database controls entitlements. Preserve historical purchases and certificates after cancellation. Subscription cancellation should default to period-end. Do not encode legal usage rights solely in Stripe product names. Return verified webhook events to the entitlement service for subscription started, upgraded, downgraded, payment failed, cancelled and one-off purchased.

### Download/auth developer

> Build a versioned pack-delivery system using authenticated entitlement checks and expiring signed URLs. Record every successful download with user, organization, pack, version, entitlement, plan and timestamp. Generate or associate a unique license certificate for each qualifying download/purchase. Creator/Pro users lose new download access after their paid term expires but retain account history and certificates. One-off purchasers retain access to the purchased pack/version. Do not build DRM or browser-only asset editing.

### Copywriter

> Write BBCO copy as an intelligent production resource, not a trendy design startup. Short sentences. Clear rights language. Avoid hype such as revolutionary, limitless, game-changing or legally safe. Never imply that fictional catalogue brands are operating consumer companies. Core line: “Brands built to live inside other stories.” Campaign platform: “You’ve seen it before. You just haven’t.” Product language should repeatedly emphasize believable worlds, production-ready files, printability, licensing clarity and saved production time.

---

## K. Launch checklist

### Product
- [ ] Five packs pass Scene-Ready Pack Standard.
- [ ] Every public brand name has a clearance record.
- [ ] ZIPs have manifests and versions.
- [ ] Physical print tests completed.
- [ ] Preview assets watermarked appropriately.

### Commerce
- [ ] Creator checkout works.
- [ ] Pro checkout works.
- [ ] One-off checkout works.
- [ ] Studio inquiry works.
- [ ] Stripe webhook failures tested.
- [ ] Period-end cancellation tested.
- [ ] Failed-payment behavior tested.

### Entitlements
- [ ] Subscription entitlement works.
- [ ] One-off entitlement works.
- [ ] Signed URLs expire.
- [ ] Download logs persist.
- [ ] Cancelled Creator/Pro behavior is correct.
- [ ] Studio manual override process exists.

### Licensing
- [ ] Production License reviewed by counsel.
- [ ] Terms reviewed.
- [ ] Privacy reviewed.
- [ ] Website explainer matches controlling license.
- [ ] Certificates store/display correct license revision.
- [ ] Fictional-brand disclaimer displayed.

### Account
- [ ] History survives cancellation.
- [ ] Certificates survive cancellation.
- [ ] Billing portal works.
- [ ] Empty/error states exist.

### Analytics
- [ ] Checkout events recorded.
- [ ] First download recorded.
- [ ] Scene-filter usage recorded.
- [ ] Cancellation recorded.
- [ ] No sensitive production files exposed through analytics.

### Brand
- [ ] Locked BBCO wordmark used.
- [ ] Shared Spine BB used only as secondary mark.
- [ ] Parent palette respected.
- [ ] Catalogue color does not contaminate umbrella identity.
- [ ] Mobile favicon/monogram tested.

### Validation
- [ ] Minimum 20 professionals invited.
- [ ] At least 5 actual scene tests sought.
- [ ] Feedback process ready.
- [ ] No public launch before validation review.

### This week — 7 actions

1. Create the website data model on paper first: `User / Organization / Pack / PackVersion / Subscription / Purchase / Entitlement / Download / Certificate`.
2. Lock the one-off test price at `$69`.
3. Put the five launch pack records into a simple catalogue table with working title, category, scene tags, version and clearance status.
4. Have counsel answer the four code-blocking questions:
   - Creator/Pro post-cancel use
   - Studio continuing use
   - one-off ongoing-use/version scope
   - certificate assertions
5. Wireframe only four screens first:
   - Home
   - Pack
   - Pricing
   - Account / Downloads
6. Build a working Stripe → entitlement → signed-download proof of concept using one dummy pack before polishing UI.
7. Create the first certificate template: `BBCO-[PACK]-[SERIAL]-V1`, with licensee, pack, version, plan, date and permitted distribution.

### Technical milestone

Do not move beyond Week 1 until this works end to end:

**pay → entitlement row → authorized dummy-pack download → logged download event → certificate record/PDF → cancel without deleting historical records**
