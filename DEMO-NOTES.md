# Demo notes — Rev. Christy Snow homepage concept

`index.html` is fully self-contained (inline CSS + JS, no build step). It opens by
double-clicking and can be dropped as-is onto Netlify / Cloudflare Pages. The only
external resource is Google Fonts (Fraunces + Newsreader), which degrades gracefully
to system serifs offline.

---

## A. Placeholder images to supply before presenting

Every placeholder is a clearly-labeled block on the page. Swap each for a real photo
(keep roughly the noted shape/crop):

| # | Where on the page | What to drop in | Shape |
|---|---|---|---|
| 1 | **Hero** (the big arch) | ✅ Done — supplied portrait was background-removed (macOS Vision subject-lift), edge-feathered, and embedded as an inline WebP so the page stays a single file. For production, serve it as a real image file instead (see the `PRODUCTION-WIRING` comment at the hero figure). | Tall 3:4 |
| 2 | Services → Living In Solution | Retreat-circle / teaching photo | Small arch, 3:3.6 |
| 3 | Services → Retreats | NC foothills landscape (retreat setting) | Small arch |
| 4 | Services → One-on-One Guidance | A one-on-one conversation photo | Small arch |
| 5 | Services → Speaking | Keynote / stage photo (Charlotte Pride, interfaith service…) | Small arch |
| 6 | About (side arch) | Rev. Christy teaching or in ministry | Tall arch, 3:3.8 |
| 7–10 | Music list (4 squares) | Album art: *Path To Oneness*, *Free To Be*, *Peaceful Journey*, *Attune To The Ancients* | Small squares, 56px |

Implementation: each placeholder is a `div.arch` / `span.cover` — replace the inner
label with an `<img>` (add real `alt` text), or set the photo as a `background-image`
on the block. The arch mask and gold keyline already handle the styling.

Also worth supplying for production (not blocking the demo): a 1200×630 social-share
card (`og:image`) and exact pull-quotes from the Creative Loafing / Queen City Nerve
pieces — the press section currently uses honest *restatements* of her recognition,
flagged with an HTML comment, and should be upgraded to verbatim quotes before launch.
(The k.d. lang / Natalie Merchant / Tracy Chapman voice comparison comes from her bio
materials, not a documented article — source it or keep it attribution-free.)

## B. Where a real backend / booking gets wired in

Each spot is marked in the source with a `<!-- PRODUCTION-WIRING: ... -->` comment:

1. **Email capture form** (`#signup`, the "A note at first light" band) — markup is a
   real `<form>` with name + email. Point it at Mailchimp / Flodesk / Buttondown
   (embed or POST endpoint) and delete the demo submit-handler in the `<script>` at
   the bottom. Labels, focus states, and the success state are already built.
2. **Living In Solution CTA** ("Schedule a free consultation") — currently a `mailto:`
   to booking@christysnow.com. Production: a consultation form or scheduler (Calendly
   or similar), plus real next-cohort dates. The badge says "Next circle — inquire to
   join" (true regardless of enrollment state); if Christy confirms a cohort is
   actually forming, switch it to the stronger "Next circle now forming" (see the
   `CONTENT-VERIFY` comment in the source).
3. **Retreats CTA** ("Plan your retreat") — currently `mailto:`. Production: rebuild the
   existing Awaken Within booking-form fields (name, email, phone, retreat type, dates)
   on-site.
4. **Coaching + Speaking CTAs** — currently `mailto:` with pre-filled subjects; could
   stay mailto or become short inquiry forms.
5. **"Full calendar" link** (Live section) — points at the existing
   christysnow.com/calendar for now; in the rebuild the calendar lives on-site.
6. **Analytics** — none included (it's a demo). Add GA4 / a privacy-friendly
   alternative at launch; her current site has zero tracking, an easy talking point.

## C. Talking points baked into the demo (for the pitch meeting)

- **Hierarchy flipped:** the year-long course is the hero CTA and the double-scale
  lead feature; music is one elegant dark section, not a wall of $10 CDs.
- **One hub:** footer unifies all four web properties + streaming + socials, with one
  clickable contact email (her current site's email isn't even a link).
- **Fixes the audit's technical debt by example:** `lang` attribute, one `h1`, real
  meta description, favicon, alt text/ARIA on imagery, AA color contrast,
  `prefers-reduced-motion` support, mobile-first layout.
- All offerings, press recognition, names, dates, and the Jun 13 Golden Road Vineyard
  show are real, from the audit; only the photos and the form backend are stand-ins.
