# Demo notes — Rev. Christy Snow homepage concept

`index.html` is fully self-contained (inline CSS + JS, no build step). It opens by
double-clicking and can be dropped as-is onto Netlify / Cloudflare Pages. The only
external resource is Google Fonts (Fraunces + Newsreader), which degrades gracefully
to system serifs offline.

---

## A. Images — all 10 slots are now filled with real assets

Every image is embedded inline (WebP data URI) so the demo stays one portable file.
Nothing is hotlinked from her live sites. Sources and treatments:

| # | Slot | What's in it now | Notes |
|---|---|---|---|
| 1 | Hero arch | Supplied portrait, background-removed (macOS Vision subject-lift) + edge-feathered into the dawn gradient | — |
| 2 | Living In Solution | Outdoor retreat-practice circle (from awakenwithin.me) | Good fit for "retreat-style Saturdays" |
| 3 | Retreats | Cabin + hammock in the woods (from awakenwithin.me) | ⚑ Likely stock on her Wix site — an authentic photo of her real venue (Riversong Cabins, Elkin NC) would beat it |
| 4 | One-on-One Guidance | "Coaching Christy" portrait (from awakenwithin.me) | A candid two-person shot would read even more "1:1" |
| 5 | Speaking | **Interfaith Thanksgiving service, 2014** (per your pick), cropped to the podium side and warm-duotoned (espresso/ivory) to blend with the palette | Original is B&W, 564×196 — low-res but fine at thumb size |
| 6 | About arch | Stage close-up at the mic (christysnow.com), purple stage-light cast warm-balanced to match the page | The flute close-up candidate was tried first but it's an extreme hands-detail shot — face is soft-focus, doesn't read as a portrait |
| 7 | Path To Oneness | Supplied elephant artwork | — |
| 8–10 | Free To Be / Peaceful Journey / Attune To The Ancients | 600² covers from her site's CDN | — |

**Licensing:** these are Christy's own promotional photos and album art — fine for
her rebuild pitch, but confirm photographer credits/usage rights before launch.
For production, serve images as real files with `srcset` instead of inline base64
(see `PRODUCTION-WIRING` comments).

Also worth supplying for production (not blocking the demo): a 1200×630 social-share
card (`og:image`) and exact pull-quotes from the Creative Loafing / Queen City Nerve
pieces — the press section currently uses honest *restatements* of her recognition,
flagged with an HTML comment, and should be upgraded to verbatim quotes before launch.
(The k.d. lang / Natalie Merchant / Tracy Chapman voice comparison comes from her bio
materials, not a documented article — source it or keep it attribution-free.)

## B. The "still in the unmanifest" preview page (`preview.html`)

Every link that used to open an email client (or eject to her old site) now lands on
one shared, fully designed preview page. The top of the page is the same everywhere —
*"This page is still in the unmanifest."* with a little ember sun waiting under the
horizon line — and a swappable panel describes what that specific page becomes in the
full build. A `?p=` URL parameter picks the blurb (plain JS, no build step; unknown or
missing keys fall back to a generic blurb, so there's no way to break it).

Current wiring (homepage link → preview variant):

| Homepage link | URL | Blurb describes |
|---|---|---|
| "Schedule a free consultation" (Living In Solution) | `preview.html?p=living` | The course page: the year month by month + application that books the free consultation |
| "Plan your retreat" | `preview.html?p=retreats` | The retreats funnel page → toward Living In Solution + simple inquiry |
| "Start the conversation" (coaching) | `preview.html?p=coaching` | The coaching page + easy first-conversation booking |
| "Invite Christy" (speaking) | `preview.html?p=speaking` | The speaking page + short booking form for organizers |
| "Full calendar" (Live section) | `preview.html?p=calendar` | The on-site shows calendar (no more sending fans to a separate platform) |
| "Book the band" | `preview.html?p=band` | The live-music booking page for venues & event hosts |
| "Booking & contact" (footer) | `preview.html?p=contact` | The contact page: one working form instead of a copy-paste email |

To add another variant: add a key to the `BLURBS` map at the bottom of `preview.html`
and link to `preview.html?p=<key>`. Nav links and footer "The Work" links still scroll
to their homepage sections (those sections exist, so no preview needed).

## C. Where a real backend / booking gets wired in

Each spot is marked in the source with a `<!-- PRODUCTION-WIRING: ... -->` comment:

1. **Email capture form** (`#signup`, the "A note at first light" band) — markup is a
   real `<form>` with name + email. Point it at Mailchimp / Flodesk / Buttondown
   (embed or POST endpoint) and delete the demo submit-handler in the `<script>` at
   the bottom. Labels, focus states, and the success state are already built.
2. **Living In Solution CTA** — the preview link becomes a consultation form or
   scheduler (Calendly or similar), plus real next-cohort dates. The badge says
   "Next circle — inquire to join" (true regardless of enrollment state); if Christy
   confirms a cohort is actually forming, switch it to the stronger "Next circle now
   forming" (see the `CONTENT-VERIFY` comment in the source).
3. **Retreats CTA** — the preview link becomes the on-site retreat booking form
   (rebuild the existing Awaken Within fields: name, email, phone, retreat type, dates).
4. **Coaching + Speaking CTAs** — preview links become short inquiry forms.
5. **"Full calendar" / "Book the band"** — preview links become the on-site calendar
   page and the live-music booking page.
6. **Footer "Booking & contact"** — preview link becomes the contact page with a real
   form posting to one inbox.
7. **Analytics** — none included (it's a demo). Add GA4 / a privacy-friendly
   alternative at launch; her current site has zero tracking, an easy talking point.

## D. Talking points baked into the demo (for the pitch meeting)

- **Hierarchy flipped:** the year-long course is the hero CTA and the double-scale
  lead feature; music is one elegant dark section, not a wall of $10 CDs.
- **One hub:** footer unifies all four web properties + streaming + socials, with one
  clickable contact email (her current site's email isn't even a link).
- **Fixes the audit's technical debt by example:** `lang` attribute, one `h1`, real
  meta description, favicon, alt text/ARIA on imagery, AA color contrast,
  `prefers-reduced-motion` support, mobile-first layout.
- All offerings, press recognition, names, dates, and the Jun 13 Golden Road Vineyard
  show are real, from the audit; only the photos and the form backend are stand-ins.
