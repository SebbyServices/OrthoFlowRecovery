# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Read this file first, every session, before touching code.

---

## START HERE: Session Bootstrap

**Last session: 2026-09-05.** The signed services agreement arrived this session (client
countersigned 2026-09-04). The deposit is paid and the engagement is a **go**. This
session did the structural rebuild the agreement requires, and then a second, larger
one: **the repo root is no longer the three-page site.**

**The full three-page build now lives under `preview/`** (`preview/index.html`,
`preview/about.html`, `preview/surgeons.html`), and the **repo root `index.html` is now
the agreement's Section 2 holding page**: logo, phone, service area, "Now Taking
Reservations." This split exists because GitHub Pages can only serve one thing at the
domain root, and Sebby is wiring DNS this same session so the custom domain will start
resolving here. Read "Two site areas" under Architecture before assuming `index.html`
is still the homepage, it is not anymore.

**All content under `preview/` is still `[placeholder]`**, and every page there still
carries `noindex`. The root holding page is real, approved content and is deliberately
**not** `noindex`.

**The agreement changed the scope of page 3 and added real HIPAA-shaped constraints on
the forms. Both are scaffolded under `preview/`, neither has real page copy.** Read
"Page 3: Culture is retired" and "Enquiry forms" below before adding content to
`preview/surgeons.html` or either form.

**Two facts that were blocking contact details are now resolved, and both gates have
cleared.** See `PRIVATE_NOTES.local.md` for the specifics, this file only states what's
safe publicly: the phone number question has an answer and the verification step that
was blocking publication is done, the service area is confirmed, and the phone number
now appears on the live holding page. The client's address must still never be
published, that has not changed.

**Domain status: DNS wiring in progress.** `orthoflowrecovery.com` is registered
through a GoDaddy account that also runs the client's live Microsoft 365 business
email. Sebby has registrar access and is switching the site's A/AAAA/CNAME records from
GoDaddy's own Website Builder to GitHub Pages this session. **Do not touch, and do not
assume anyone else has touched, the MX records or either TXT record (SPF and the
Microsoft 365 verification string) or the `_dmarc` TXT record.** Those are live email
and are not part of this change. See "DNS and Deploy" below for the exact record set
and what this domain's zone actually contains, confirmed by screenshot this session.

### 1. Orient (run these first, in order)

```bash
git log --oneline -4          # expect d900777, 7452c5a, 82d5f9a, 415ec9a, this session's work is uncommitted
git status --short            # expect the holding-page split: renames plus edits, NOT clean
git fetch -q origin && git rev-list --left-right --count origin/main...main   # expect 0 0 before committing
python3 -m http.server 8000   # holding page at :8000/, full build at :8000/preview/
curl -s -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com          # holding page once DNS clears
curl -s -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com/preview/ # full build, once DNS clears
```

### 2. Where things actually stand

| Area | State |
|---|---|
| Agreement | **Signed 2026-09-04.** Engagement is paid and active. Commercial terms live only in `PRIVATE_NOTES.local.md` and the ops folder, never here |
| Repo root `index.html` | **The holding page, as of this session.** No longer the site homepage. See "Two site areas" under Architecture |
| Full 3-page build | **Moved to `preview/`** this session: `preview/index.html`, `preview/about.html`, `preview/surgeons.html`. Page 3 rebuilt to spec ("For Surgeons & Practices"), matching the signed agreement. Not yet committed |
| Page 3 content | **Scaffolded, not written.** Sections exist for what OrthoFlow handles, what the office doesn't manage, how to refer, coverage/response, a compliance-note placeholder, and the practice form. All still `[placeholder]` |
| `styles.css` / `main.js` | Ported and working. Two small additions this session: `.form-notice` for the required medical-information notice on both forms, and an inline `<style>` block scoped to the root holding page only, see Architecture |
| Nav / mobile menu / footer | Rebuilt across all three `preview/` files this session: "Culture" is now "For Surgeons" (nav/mobile) and "For Surgeons & Practices" (footer). The intended `#reserve` asymmetry is preserved, re-verify with the Commands sweep before committing |
| Heading structure | Still fixed, one `<h1>` per page under `preview/`, plus one on the new root holding page |
| Client copy in HTML | **None under `preview/`.** Every headline and paragraph there is `[placeholder]`. The root holding page is real, approved copy, see below |
| `CONTENT_DECK.md` | Updated this session to match the signed agreement: confirmed facts, the new page 3 outline, vision/mission/values moved under About, and the pending Patient Brokering Act compliance line. The old "Culture Page" draft is marked superseded, not deleted |
| Logo / favicon | Real, unchanged since 2026-08-26. Five derived web assets are confirmed client-owned regardless of payment status |
| Brand color / fonts | **Current values may be superseded.** A client-sent design direction proposes different fonts and slightly different color samples. Not yet confirmed in writing, do not change the stylesheet on this alone. See Architecture |
| Contact phone | **Both gates cleared this session.** Live on the root holding page as a real `tel:` link. See `PRIVATE_NOTES.local.md` for the number itself, this file does not restate it |
| Service area | **Confirmed**, and live on the root holding page. See `PRIVATE_NOTES.local.md` for the exact wording used elsewhere |
| Business hours | Still not supplied |
| Enquiry forms | **Scaffolded this session, not wired, both under `preview/`.** Home's reserve form now uses a timing-range picklist instead of a procedure-date field, and the free-text notes field was removed. The new practice form on `preview/surgeons.html` collects name/phone/email only. Both show the required medical-information notice. Neither has a real Formspree endpoint yet |
| Formspree form | **Deliberately unwired.** `REPLACE_WITH_ORTHO_FLOW_FORM_ID` (reserve) and `REPLACE_WITH_ORTHO_FLOW_PRACTICE_FORM_ID` (practice), one endpoint needed per form |
| Product / device line | NICE, confirmed. Exact model and manufacturer photography rights still open |
| Search indexing | `noindex, nofollow` on all three `preview/` pages. **The root holding page deliberately has no `noindex`**, see Architecture. Remove `preview/`'s `noindex` at launch |
| Domain / DNS / Pages | GitHub Pages LIVE and built on `github.io`. **DNS wiring in progress this session**, see "DNS and Deploy." The domain also carries live Microsoft 365 business email, confirmed by zone screenshot, not to be touched |
| Holding page | **Built this session**, at the repo root. Logo, phone, service area, "Now Taking Reservations." No pricing, no clinical claims, per the agreement's Section 2 spec |
| Pushed to GitHub | Not yet. This session's rebuild is local only, see `git status` |

### 3. Ask Sebby before doing anything else

These are open decisions, not tasks. Do not resolve them by guessing.

1. **Font and color confirmation.** A design direction has been proposed but not
   confirmed in writing. Do not touch `styles.css` typography or color tokens until it
   is.
2. **Positioning against the sibling client**, beyond what the signed agreement already
   locks in structurally (distinct palette, no cross-links). How the two market
   relative to each other in an overlapping metro area is still open.

Resolved this session: the page 3 structural rename (scaffolded ahead of copy), and the
holding page (built at the repo root once both the phone-ownership and business-listing
gates cleared). See Architecture for both.

Specifics behind all four, plus everything about the sibling client relationship and
the phone number, are in `PRIVATE_NOTES.local.md`. Read that file before acting on any
of them. It is gitignored on purpose because this file is public.

### 3b. Client supplied material: handle in the private notes

Several things have arrived from the client that cannot be summarized in a tracked
file: contact and address details, a document marked private containing identifiable
patient health information, and a non-binding design direction document. All are
written up in `PRIVATE_NOTES.local.md`.

The operative rules here, which are safe to state publicly:

- The phone number and service area are confirmed and now live on the root holding
  page. That does not extend to `preview/`, which stays placeholder until the client
  approves real copy there.
- The client's business address is never published. The default is the service area
  in its place, everywhere a street address might otherwise go.
- No client supplied testimonial, quote, or patient video goes on this site. Not
  paraphrased, not anonymized by first name alone. The default is no, and changing that
  needs written per patient marketing authorization and a legal read, not a judgment
  call made here. This is now also a signed contractual term, not just a house rule.
- Neither enquiry form may collect free-text medical information, a procedure or
  surgery date, a symptom or diagnosis field, or an insurance field. Both display a
  short notice asking the visitor not to include medical information and offering a
  phone call instead. This is a signed contractual term: the site is built so it never
  collects Protected Health Information, and the developer is not a HIPAA business
  associate. Do not add a form field that would change that without raising it first.
- Do not restate the contents of any private document, or any commercial term, in any
  tracked file, commit message, or comment.

### 4. Work that is UNBLOCKED right now

Safe to do without any further client input:

- Responsive QA at 375px, 768px, 1280px on all three pages
- Keyboard-only tab pass, confirm focus states are visible
- Confirm no section is stuck at `opacity: 0` (see the fade-in note below)
- Lighthouse pass on structure and accessibility
- Tighten semantics or ARIA where the ported markup is weak
- Update `CONTENT_DECK.md`'s factual fields (service area, business basics) to match
  what's now confirmed, without inventing any page copy
- Structural work on `preview/surgeons.html` and either form's markup, so long as no
  real copy, pricing figure, or compliance-line wording goes in without approval

### 5. Work that is BLOCKED

Do not start these, and do not invent content to unblock them:

- Any real copy for any `preview/` page. The client approves it in `CONTENT_DECK.md`
  line by line, then it goes in
- Publishing the client's street address, ever, absent his written instruction
- Business hours, exact device model
- Formspree form creation and IDs for either enquiry form
- Hero photo or video
- Any change to `styles.css` fonts or color tokens, pending written confirmation
- The Patient Brokering Act compliance line on page 3, without a healthcare attorney's
  review first
- Social handles, which is why the footer social icons are commented out

### 6. Standing rule for this repo

If a task would make this site read or look like Elite Care Recovery, stop and raise it.
See "Hard Separation" below. That section is the most important part of this file. It is
now also a signed contractual commitment, not just an internal convention.

---

## Project Snapshot

- **Client:** Ortho Flow Recovery (Miami-Dade and Broward, FL)
- **Business:** Post-operative recovery equipment rental, with a second audience of
  referring surgeons and practices, not just patients
- **Owner contact:** see `PRIVATE_NOTES.local.md`
- **Engagement:** signed and paid, see `PRIVATE_NOTES.local.md` for terms. Commercial
  specifics never belong in this file
- **Domain:** `orthoflowrecovery.com`, registered, **not wired to this repo**
- **Repo:** `github.com/SebbyServices/OrthoFlowRecovery`, **public**
- **Developer:** Sebby IT Consulting, Corp.
- **Status:** Site unchanged since 2026-08-26, still all placeholder copy. The
  engagement itself has moved substantially: signed agreement, confirmed facts, a new
  page 3 scope, and new form constraints, none yet reflected in the HTML.

**Relationship to the sibling client:** There is a second, separate client in a separate
repo operating in the same space. Treat the two as distinct businesses that may compete.
The specifics of who they are to each other are in `PRIVATE_NOTES.local.md`, not here,
because this file is public. See "Hard Separation" below. This is not optional.

---

## Hard Separation from Elite Care Recovery

This skeleton borrowed Elite Care's **architecture and design system only**. Everything
below is forbidden to carry across:

- **Never copy the sibling client's prose.** Their homepage story describes a shared
  family business. It cannot be reused to describe this separate company.
- **Never reuse the Elite Care Formspree ID (`xeedwqvp`).** It routes leads into Elite
  Care's inbox. Ortho Flow needs its own form, for each of its two enquiry forms. The
  placeholder in `preview/index.html` is `REPLACE_WITH_ORTHO_FLOW_FORM_ID`.
- **Never reuse an Elite Care phone number** or any `@elitecarerecovery.net` address.
  The specific numbers live in `PRIVATE_NOTES.local.md`, which is gitignored. Do not
  write client contact details into any tracked file. See "This repo is public" below.
- **Never copy Elite Care or NICE product assets.** The NICE1 is a manufacturer product
  sold through a national dealer network, not Elite Care's exclusive line. Neu Medical
  DME in Minnesota sells the same device, and so does the sibling client, so the two
  sites cannot differentiate on hardware at all. Differentiation has to come from
  service, delivery, and support. Product photography still belongs to NICE or to
  whichever dealer commissioned it. Never lift product images from another dealer's
  site. Ask whether NICE publishes an authorized dealer asset kit instead.
- **Never copy `CONTENT_DECK.md` from the Elite Care repo.** That is their approved
  client content.
- **Distinct color palette and type treatment from Elite Care's, always.** This is now
  a signed contractual commitment (Section 11 of the agreement, see
  `PRIVATE_NOTES.local.md`), not just a house convention. If the pending font and color
  direction (see Architecture) ever converges visually with Elite Care's site, that is
  a problem to raise, not a coincidence to let ride.
- **No links between the two sites**, unless both clients agree in writing. Also now a
  signed term.

If a change would make the two sites look or read alike, stop and raise it.

---

## Tech Stack: LOCKED

Same rationale as the Elite Care build: non-technical client, static hosting, handoff
must be readable by any web dev.

- Plain HTML5 + CSS3 + vanilla JS
- No build step, no npm, no bundler, no framework
- Single `styles.css`, single `main.js`
- Google Fonts via `<link>`, currently Playfair Display + Inter. **A client-sent design
  direction proposes Poppins + Source Sans 3 instead, not yet confirmed in writing.**
  Do not swap fonts on the strength of that document alone, see Architecture
- Inline SVG icons only
- Form: Formspree (free tier), IDs not yet provisioned for either enquiry form

---

## Commands

There is no build, no lint, and no test runner. These are the checks that stand in for
them. Run all three sweeps before every commit that touches markup.

```bash
# Serve locally, then open http://localhost:8000. Holding page at /, full build at
# /preview/. No build step, just refresh.
python3 -m http.server 8000

# 1. Shared-chrome drift, WITHIN preview/ only. The root holding page has no nav,
#    mobile menu, or footer, so it is not part of this sweep. Expect exactly THREE
#    diffs per subpage, all of them the intended `index.html#reserve` asymmetry: one in
#    nav, one in the mobile menu, one in footer. Anything else is real drift.
cd preview
for block in nav footer; do
  for page in about surgeons; do
    echo "== $block: index vs $page =="
    diff <(sed -n "/<$block>/,/<\/$block>/p" index.html) \
         <(sed -n "/<$block>/,/<\/$block>/p" $page.html)
  done
done
# The mobile menu is NOT inside <nav>, so it needs its own diff, against BOTH subpages.
for page in about surgeons; do
  echo "== mobile-menu: index vs $page =="
  diff <(sed -n '/<div class="mobile-menu">/,/<main/p' index.html) \
       <(sed -n '/<div class="mobile-menu">/,/<main/p' $page.html)
done
cd ..

# 2. Em dash sweep, whole repo, INCLUDING PRIVATE_NOTES.local.md. Rule 10 below applies
#    there too. Must print nothing. Use `command grep`, not plain `grep`: in this shell
#    `grep` is wrapped to respect .gitignore by default, so a plain recursive `grep -r`
#    silently skips PRIVATE_NOTES.local.md and reports a false pass. Confirmed
#    2026-09-05: `type grep` showed a ugrep wrapper with `--ignore-files`.
LC_ALL=C command grep -rn $'\xe2\x80\x94' --include='*.html' --include='*.css' --include='*.js' --include='*.md' .

# 3. Pre-launch readiness, preview/ only. MUST be zero before launch. The pattern
#    deliberately skips the legitimate `.image-placeholder` class. The root holding
#    page is excluded on purpose, it is real approved copy, not a placeholder.
grep -rc '\[.*placeholder\|TODO\|REPLACE_WITH' preview/index.html preview/about.html preview/surgeons.html styles.css
```

Verify the four `#reserve` links per subpage directly, since sweep 1 only covers two of
them:

```bash
cd preview
grep -n 'href="index.html#reserve"' about.html surgeons.html   # expect 4 per file
grep -n 'href="#reserve"' index.html                            # expect 4
cd ..
```

**Note:** `culture.html` was renamed to `surgeons.html` on 2026-09-05, and the whole
three-page build moved from the repo root into `preview/` the same session, when the
repo root became the holding page instead. Every sweep above was updated to match. If
you see a bare `index.html`/`about.html`/`surgeons.html` reference outside `preview/`
in this file again (other than the root holding page's own `index.html`), it's drift.

---

## Architecture

Three flat HTML pages sharing one stylesheet and one script, plus, as of 2026-09-05, a
fourth standalone page at the repo root.

### Two site areas: the holding page at root, the full build under `preview/`

GitHub Pages serves whatever `index.html` sits at the repo root, and only that, so the
holding page and the three-page marketing site cannot both live there. As of
2026-09-05:

- **Repo root `index.html`** is the agreement's Section 2 holding page: logo, phone,
  service area, "Now Taking Reservations." No nav, no footer, no shared chrome, it
  shares `styles.css` for tokens and fonts only, plus a small inline `<style>` block
  scoped to itself. Deliberately **not** `noindex`, since it's meant to be found during
  the client's active outreach. It gets overwritten entirely at launch.
- **`preview/`** holds the actual three-page marketing site: `preview/index.html`,
  `preview/about.html`, `preview/surgeons.html`, still sharing the root `styles.css`
  and `main.js` (referenced via `../`). Every page there still carries `noindex`, since
  it's all still `[placeholder]` copy. This matches the "preview address that is public
  but unlisted" language in the signed agreement, it is not linked from the holding
  page and carries no confidential content, just unapproved copy.

**When this changes again, at launch:** the plan is to promote `preview/`'s three files
back up to the repo root (reversing this move) and retire the holding page, not to
leave both living side by side indefinitely. Do that as one deliberate pass, re-running
every sweep below with paths restored to root.

### Page 3: Culture is retired, `surgeons.html` replaces it

The signed agreement specifies **Home, About, and "For Surgeons and Practices"** as the
three pages, all now under `preview/`. `culture.html` was renamed to `surgeons.html` on
2026-09-05, preserving git history via `git mv`, then the whole directory moved under
`preview/` the same session, see "Two site areas" above. Vision, mission, and values
moved into `preview/about.html` rather than disappearing, see that page's new sections
between "Why Ortho Flow" and the CTA band.

The new page 3 is addressed to a different reader entirely: surgeons, practice managers,
surgical coordinators, and ASC or discharge staff, not patients. Built sections, all
still placeholder text: what OrthoFlow handles, what the referring office does not have
to manage, a three-step "how to refer" card row, coverage and response times, a
compliance-note placeholder, and the practice enquiry form.

**A required compliance line belongs in the compliance-note section**, exact wording
tracked in `CONTENT_DECK.md` since it is future public copy, not a confidential detail.
It needs a healthcare attorney's review before publishing. Do not fill that section in
from general marketing instinct, and do not draft additional referral-incentive language
anywhere else on this page either.

**Structure is done, content is not.** The page exists under `preview/`, the
nav/mobile-menu/footer edits landed in all three `preview/` files, and the Commands
sweeps were updated to reference `preview/surgeons.html`. What's still missing: real
copy (gated on facts from the client), the compliance line (gated on attorney review),
and the practice form's Formspree endpoint.

### Enquiry forms: two now, both field-restricted, both scaffolded

The signed agreement specifies two forms and constrains both, and both are now built to
that spec:

- Fields allowed: name, phone, email, and, **on the reserve form only**, a non-clinical
  timing range picklist ("within 2 weeks," "2 to 6 weeks," "6 or more weeks," "not sure
  yet"), built as a `<select>`.
- **Never add:** a free-text medical field, a specific surgery or procedure date, a
  symptom or diagnosis field, an insurance field, or anything else that combined with
  the business's identity would reveal a health event about a named person. The reserve
  form used to have both a date field and a free-text notes field, in violation of the
  signed agreement's own field list. Both were removed on 2026-09-05.
- Both forms show the required notice, styled by the new `.form-notice` rule in
  `styles.css`: "Please do not include medical information in this form. We will
  contact you to discuss any specifics by phone."
- This is a signed contractual term, not a style preference. The site is built so its
  public forms never collect Protected Health Information, and submissions must never
  route to any developer-controlled inbox or system. Changing a form field in a way that
  would collect PHI is out of scope of the current agreement and needs a separate
  written change order first.

Each form still needs its own Formspree endpoint, in the client's own account, per the
existing rule that the client owns every enquiry. The reserve form's placeholder is
`REPLACE_WITH_ORTHO_FLOW_FORM_ID`, the practice form's is
`REPLACE_WITH_ORTHO_FLOW_PRACTICE_FORM_ID`. Never reuse one for the other.

### The nav, mobile menu, and footer are copy-pasted into all three pages

This applies within `preview/`, which has no templating either. Any change to `<nav>`,
`.mobile-menu`, or `<footer>` must be applied **three times**, once per file under
`preview/`. This was the #1 regression source on the Elite Care build. See "Commands"
above for the full sweep. The page 3 rename touched all three files' nav labels and
footer links on 2026-09-05, in addition to `surgeons.html` itself. The root holding
page has none of this shared chrome, see "Two site areas" above.

The only **intended** divergence: the reserve form lives on the homepage, so subpages
link `index.html#reserve` where the homepage links `#reserve`. This happens in **four**
places per subpage:

| # | Location | Caught by sweep 1? |
|---|---|---|
| 1 | nav CTA | yes, in the `nav` diff |
| 2 | mobile menu CTA | no, `.mobile-menu` is outside `<nav>`, needs its own diff |
| 3 | bottom CTA band button (`section.bg-accent`) | no, it is page body, not shared chrome |
| 4 | footer quick link | yes, in the `footer` diff |

Preserve that asymmetry. Making them identical breaks the subpage CTAs. Two of the four
are invisible to the shared-chrome sweep, so check them with the `grep` above.

### `.mobile-menu` sits outside `<nav>` on purpose

A positioned ancestor traps the fixed overlay. Do not move it back inside `<nav>`.

### Section backgrounds are class-driven, never inline

| Class | Effect |
|---|---|
| `section.bg-cream` | `--color-bg` |
| `section.bg-cream-alt` | `--color-bg-alt` |
| `section.bg-charcoal` | charcoal bg, white text, gold eyebrows |
| `section.bg-accent` | accent bg, white text. Bottom CTA bands on About/surgeons page |

Note the token rename carried over from the Elite Care build: `--color-blue` is
`--color-accent` here, and `.bg-blue` is `.bg-accent`. Keep the neutral token names
regardless of what happens with the actual color values below.

**Brand color currently lives in exactly one place**, `--color-accent` and
`--color-accent-dark` in `styles.css`, sampled from the client's logo. **A client-sent
design direction proposes slightly different samples** (resampled from what may be a
higher-resolution source file) **and an expanded palette** with new named tokens for
page ground, cards, and borders. That document explicitly frames itself as "a direction,
not a specification" pending the client's written confirmation, which has not arrived.
Do not change any color token on the strength of that document alone. When confirmation
does arrive, reconcile the exact values against what's in `PRIVATE_NOTES.local.md` rather
than re-deriving them from scratch.

### Layout primitives

| Selector | Behavior |
|---|---|
| `.container` | `max-width: 1200px`, centered, 1.5rem side padding |
| `section` | vertical rhythm only, `padding: clamp(4rem, 8vw, 8rem) 0` |
| `.split-50-50` | one column until 1024px, two above it |
| `.card-grid` | the benefit and step card rows |
| `.eyebrow` | uppercase gold kicker above every `<h2>` |
| `.image-placeholder` | the in-repo stand-in for missing client photography |

### `main.js`: five behaviors, no framework, no DOMContentLoaded

Sticky nav at 50px, mobile menu, smooth scroll, Formspree submit, IntersectionObserver
fade-in, plus `setActiveNavLink()`. The script is loaded at the end of `<body>`, which is
why it needs no `DOMContentLoaded` wrapper. Do not move it into `<head>` without adding
`defer`.

Three things that surprise people:

1. **The fade-in CSS is injected at runtime.** `main.js` appends a `<style>` block
   defining `.fade-out` / `.fade-in` / `@keyframes fadeInUp`. Searching `styles.css`
   finds nothing. Every `section`, `.card`, and `.step-card` starts at `.fade-out`, so
   **a section that never intersects stays invisible**.
2. **The form handler binds `document.querySelector('form')`**, the first form on the
   page only. This is still safe with two enquiry forms in the site, since the reserve
   form and the practice form live on different pages (Home and the surgeons page), and
   each page's DOM has exactly one form. It would only become a real gap if a second
   form ever landed on the same page as an existing one. It also `preventDefault()`s
   unconditionally, so while a Formspree ID is still a `REPLACE_WITH_...` placeholder,
   every submit lands in the catch branch and shows the error state. That is the
   expected behavior right now, not a bug to chase.
3. **`setActiveNavLink()` only touches `.nav-links a`.** The `.mobile-menu` links never
   receive `.active`, so the mobile overlay shows no current-page indicator.

The success message deliberately promises no response time. Do not put a time
commitment back in without the client agreeing to it in writing.

### `.hero` carries an explicit background

There is no hero media yet and the hero text is white. `.hero` sets
`background-color: var(--color-charcoal)` for that reason. Do not remove it when adding
media, layer the media on top. A client-sent design direction proposes a tap-to-call
button as the primary header action, on the reasoning that most conversions here are
phone calls, not form fills. Not yet built.

### Home page will gain a pricing section

The signed agreement specifies a pricing section on the homepage showing all rental
tiers together. **A per-day rate must never publish alone**, since it understates the
true cost after the discount period ends and would misrepresent the price. Figures are
not yet supplied. Do not build this section with placeholder numbers that look real.

---

## DNS and Deploy: read before touching the domain

GitHub Pages **is enabled and built**, serving the repository root at
`https://sebbyservices.github.io/OrthoFlowRecovery/`. Build type is `legacy` (Jekyll).

**DNS wiring started 2026-09-05.** Sebby has registrar access (GoDaddy) and is switching
the domain from GoDaddy's own Website Builder to GitHub Pages. This domain's zone was
confirmed by screenshot to carry **live Microsoft 365 business email and Teams/Skype for
Business records**, not just a hypothetical risk carried over from the Elite Care
lessons below. The confirmed zone, 20 records total, breaks down as:

- **Website-related, meant to change:** one `A @` record currently reading
  "WebsiteBuilder Site" (GoDaddy's managed pointer, not a plain IP), and one
  `CNAME www` currently pointing at the bare apex domain itself (so `www` today just
  mirrors whatever the apex resolves to). No AAAA records exist yet.
- **Email and Teams, must never be touched by this work:** three `MX @` records to
  `*.ppe-hosted.com` (Proofpoint Essentials in front of Microsoft 365), two `TXT @`
  records (an SPF line naming `_spf-usg2.ppe-hosted.com` and `secureserver.net`, and a
  `NETORGFT20691954.onmicrosoft.com` Microsoft 365 verification string), one
  `TXT _dmarc` with a `p=quarantine` policy, `CNAME` records for `autodiscover`,
  `email`, `lyncdiscover`, `msoid`, `sip`, and two `SRV` records for SIP/Teams
  federation.
- **Unrelated GoDaddy features, leave alone:** `CNAME pay` (GoDaddy payment links),
  `CNAME _domainconnect` (GoDaddy's own setup-wizard record).
- **Locked by GoDaddy already, cannot be touched anyway:** the `NS` and `SOA` records.

Check current Pages state with:

```bash
gh api repos/SebbyServices/OrthoFlowRecovery/pages \
  --jq '{status,cname,build_type,html_url}'
```

Lessons carried over from the Elite Care launch, which cost four days, plus this
domain's own specifics:

1. **Set the custom domain in ONE place**, either the Pages settings or the `CNAME`
   file, then `git pull`. Editing both churns the file. Elite Care's history has six
   `Create CNAME` / `Delete CNAME` commits from exactly this.
2. **An apex domain needs four A records AND four AAAA records.** Elite Care's apex
   certificate silently never issued because only the A records existed. GitHub reports
   no error in this state, the health endpoint returns `{}`, and the apex simply never
   appears in `.https_certificate.domains`.

   ```
   A     185.199.108.153  109.153  110.153  111.153
   AAAA  2606:50c0:8000::153  8001::153  8002::153  8003::153
   ```
3. **Disconnect the GoDaddy Website Builder site from the domain before editing the `A`
   record.** That row is a managed pointer, not a plain IP, confirmed live on this
   domain, not just an inherited warning. If GoDaddy won't let the row convert to plain
   A records while the Website Builder connection is active, unlink the product first
   under GoDaddy's My Products, not the DNS page.
4. **Point `www` at `sebbyservices.github.io` via CNAME**, replacing its current
   self-referencing setup.
5. **Do not enable Enforce HTTPS until the certificate covers every hostname you serve.**
6. **Never touch MX, either TXT record, or the `_dmarc` TXT record on this domain.**
   They are live Microsoft 365 email and DMARC enforcement, not a hypothetical. Verify
   them unchanged before and after every DNS edit, not just once.

Verify with:

```bash
# all four of these must look right before enabling HTTPS
dig +short orthoflowrecovery.com A           # expect the 4 GitHub IPs
dig +short orthoflowrecovery.com AAAA        # expect the 4 GitHub IPv6s, the one that stalled Elite Care
dig +short orthoflowrecovery.com MX          # MUST be unchanged: 3x *.ppe-hosted.com
dig +short orthoflowrecovery.com TXT         # MUST still show the SPF line and the onmicrosoft.com string
dig +short _dmarc.orthoflowrecovery.com TXT  # MUST still show p=quarantine
gh api repos/SebbyServices/OrthoFlowRecovery/pages --jq '.https_certificate.domains'
# wait until this array contains BOTH orthoflowrecovery.com and www.orthoflowrecovery.com
```

---

## Behavioral Rules

1. **Stay in the lane.** v1 is a marketing brochure site. Three pages, two forms.
2. **No copy invention.** All client-facing prose comes from an approved
   `CONTENT_DECK.md`. Until approved, placeholders stay placeholders. Do not write
   plausible-sounding marketing copy, pricing figures, or statistics to fill gaps. This
   now includes a signed contractual term against implying any operating history,
   patient count, or years in business the company does not actually have, it launched
   this month.
3. **No clinical claims, ever.** Nothing on this site may say the device reduces pain,
   swelling, or medication use. Any such wording has to come from what NICE is cleared
   to claim and must be lifted verbatim from the manufacturer. This also governs the
   client's own tagline, see Architecture, it cannot go on the site unmodified.
4. **No referral incentive language, ever**, on the surgeons and practices page.
   Nothing of value may be offered to a referral source. See "Page 3" in Architecture.
5. **Premium over clever.** White-glove medical service brand. Editorial typography,
   generous whitespace, restrained color, gold used sparingly. No gradients, neon,
   glassmorphism, or trend-chasing UI.
6. **Contrast and readability are non-negotiable.** Audience skews 50+ post-op patients,
   plus a second professional audience on page 3. Always set background and text color
   explicitly. Body text at least 17px. The current sky blue `#5DA0E2` fails WCAG AA on
   both cream and white, so it is decorative only, never text or buttons. Any future
   color values must be checked against the same rule before use.
7. **Accessibility is table stakes.** Semantic HTML, descriptive alt text, ARIA labels on
   icon-only buttons, visible focus states, skip link, labels tied to inputs.
8. **Image placeholders, not broken tags.** Use `.image-placeholder`. Never an external
   placeholder service.
9. **Mobile-first.** Min-width queries at 640/768/1024/1280. Touch targets 44x44px.
10. **Keep JS minimal.** No tracking, no analytics, no third-party scripts beyond Google
    Fonts without explicit approval. This is now also a signed contractual term.
11. **No em dashes anywhere.** Not in copy, comments, commit messages, or docs. Use a
    comma, a colon, or a full stop. When replacing one, a blind swap to a comma creates
    comma splices, so use a colon for headings and definition-style lines and a full stop
    where the next clause stands alone.

---

## Open Items Before This Can Launch

- [ ] At launch: promote `preview/`'s three files back to the repo root and retire the
      holding page, see "Two site areas" under Architecture
- [ ] Font and color confirmation from the client, in writing, before touching `styles.css`
- [ ] Healthcare attorney review of the page 3 referral-incentive compliance line
- [ ] Client sign-off on the draft copy in `CONTENT_DECK.md`, then move it into the HTML
- [ ] Pricing figures for the new homepage pricing section, supplied in writing
- [ ] Resolve every `[FACT NEEDED]` tag in the content deck. Do not guess at these
- [ ] Verify the phone number's business-listing gate, see `PRIVATE_NOTES.local.md`
- [ ] Business hours
- [ ] Create both Formspree forms and wire the real IDs, once page 3 exists
- [ ] Update `main.js`'s form handler to support two forms, not `querySelector('form')`
- [ ] Hero photo or video
- [ ] Social handles, then restore the footer social icons
- [ ] Confirm what NICE requires for logo use, product photography, and claims
- [ ] Ask the client's designer for an official reversed logo, replacing the one derived here
- [ ] Decide the holding page: build and wire DNS now, or wait for the content pack
- [x] Ortho Flow logo received 2026-08-26, web assets derived and wired in
- [x] Device line confirmed as NICE. Exact model still open
- [x] Subpage heading structure fixed, one `<h1>` per page
- [x] Dead `tel:` / `mailto:` / social anchors removed
- [x] GitHub Pages enabled and building
- [x] Service area confirmed
- [x] Phone number ownership resolved, both gates cleared, live on the holding page
- [x] Engagement signed and paid
- [x] Page 3 renamed and rebuilt to spec, nav/mobile-menu/footer updated in all three
      `preview/` files
- [x] Reserve form's field set fixed to match the signed agreement, practice form added
- [x] Holding page built at the repo root, DNS wiring underway
- [ ] **Remove `noindex, nofollow` from all three `preview/` pages at launch.** Easy to
      forget, and leaving it in means the launched site is invisible to search. The root
      holding page is deliberately exempt from this already, see Architecture

---

## Testing Checklist

The three-page items below apply to `preview/` unless stated otherwise. The root
holding page has its own short list first.

- [ ] Holding page: logo, phone, service area, "Now Taking Reservations" render
      correctly at 375px, 768px, 1280px
- [ ] Holding page: `tel:` link is a real 44px+ tap target and dials correctly
- [ ] Holding page: no `noindex` tag (intentional, unlike everything under `preview/`)
- [ ] Holding page: no pricing, no clinical claims, matching the agreement's Section 2 spec
- [ ] 375px, 768px, 1280px on all three `preview/` pages, no horizontal scroll
- [ ] Nav / mobile menu / footer edits landed in **all three** `preview/` files
- [ ] Subpages use `index.html#reserve` in all **four** spots (nav CTA, mobile menu CTA,
      bottom CTA band, footer quick link), homepage uses `#reserve`
- [ ] Every page has exactly one `<h1>`
- [ ] Sections alternate `.bg-cream` / `.bg-cream-alt` correctly
- [ ] Scroll every page fully, nothing stuck at `opacity: 0`
- [ ] Keyboard-only tab pass, focus states visible
- [ ] No console errors
- [ ] No remaining `[placeholder]`, `TODO`, or `REPLACE_WITH` text before launch
- [ ] `noindex` removed from all three pages
- [ ] Neither enquiry form has a field capable of collecting PHI, see Architecture
- [ ] Both enquiry forms show the medical-information notice
- [ ] Both enquiry forms get JS enhancement when tested on their own page (Home,
      surgeons page), since `main.js` only enhances the first form in a page's DOM
- [ ] Pricing section never shows a per-day figure alone
- [ ] Lighthouse: Performance 90+, Accessibility 95+, Best Practices 95+

---

## This repo is public, and so is everything Pages serves

The repo is public **and** GitHub Pages serves the repository root, which means every
tracked file is fetchable at the live site URL, not just the HTML.

`_config.yml` excludes the internal docs from the published site. This is verified
working:

```bash
curl -o /dev/null -w '%{http_code}\n' \
  https://sebbyservices.github.io/OrthoFlowRecovery/CLAUDE.md    # expect 404
```

**Two caveats that make this weaker than it looks:**

1. **Exclusion is not secrecy.** The files are still readable on GitHub itself, by
   anyone. It only keeps them off the site.
2. **It depends on the Pages build type staying `legacy`.** If the repo is ever switched
   to a GitHub Actions workflow build, `_config.yml` stops being honored and the internal
   docs become publicly fetchable again. Re-run the `curl` above after any Pages change.

**A signed commercial PDF briefly sat untracked in this repo's root** before anyone
noticed, one `git add .` away from being pushed public with the client's address and
both parties' signatures in it. It has been moved out. `.gitignore` now blanket-excludes
`*.pdf` and `*.docx` as a safety net, since this repo has no legitimate use for either.
**Never save a contract, invoice, or proposal into this folder, even temporarily,
even to look at it.** Read it from wherever it already lives, or copy it to the ops
folder outside any repo first.

So the rule is simple. **Client contact details, commercial terms, cross client notes,
and anything from a document a client marked private go in `PRIVATE_NOTES.local.md`,
which is gitignored.** Never in `CLAUDE.md`, `CONTENT_DECK.md`, `README.md`, an HTML
comment, or a commit message.

---

## Logo assets

The client sent one file, a 4096x2730 stacked PNG. The nav slot was built for a
horizontal wordmark at roughly 5.3:1, and the supplied lockup is 1.5:1, so dropping it
straight in would have wrecked the nav. Derived assets are committed instead:

| File | Use | Notes |
|---|---|---|
| `assets/ortho-flow-wordmark.png` | nav, mobile menu | "OrthoFlow RECOVERY" only, 4:1, no icon |
| `assets/ortho-flow-logo.png` | og:image, light backgrounds | full stacked lockup |
| `assets/ortho-flow-logo-reverse.png` | footer | navy recolored to white for the charcoal footer |
| `assets/ortho-flow-icon.png`, `favicon.png` | favicon, square uses | the circle mark alone |
| `assets/ortho-flow-logo-master.png` | source of truth | regenerate the others from this, excluded from the published site |

These five are now confirmed as the client's outright, regardless of the build's payment
status, a term added in the signed agreement.

**The current master file is a 960x640 raster copy.** It is sufficient for the web sizes
used on this site but will not support print or enlargement. If the client supplies the
original high-resolution or vector lockup, regenerate the full set from it, at no charge
per the agreement.

The reversed lockup was produced here by recoloring, not supplied by the client. Ask
the client whether his designer has an official reversed version before launch.

`.footer-logo` previously painted a white chip behind the logo to keep a dark mark
visible on the charcoal footer. That hack is gone now that a true reversed asset exists.

---

## Last Updated

- Aug 25, 2026: skeleton scaffolded from the Elite Care architecture. Design system and
  JS ported, all client copy replaced with placeholders, brand tokens genericized,
  Formspree and contact details deliberately left unwired. Committed as `cfcdb98`.
- Aug 25, 2026: added the "START HERE: Session Bootstrap" section so a cold session can
  orient without re-briefing. **Keep it current.** When the state in that table changes,
  update the table in the same commit as the change itself.
- Aug 25, 2026: pushed to the public remote at Sebby's go-ahead.
- Aug 26, 2026: client sent the logo and contact details. Brand tokens replaced with the
  real navy, logo assets derived and wired across all three pages, favicon swapped to
  PNG, `noindex` added while the live site still shows placeholder copy. Device line
  confirmed as NICE. Logged the phone number collision and the patient testimonial
  compliance block as the two things now gating contact details and social proof.
  Enabled Pages, no custom domain.
- Aug 26, 2026: `/init` audit pass. Added the "Commands" section holding the sweeps that
  stand in for a build and test suite.
- Aug 26, 2026: subpage heading structure fixed, dead anchors removed, `_config.yml`
  added to keep internal docs off the published site, draft copy written into
  `CONTENT_DECK.md` for client review.
- Aug 29, 2026: `/init` audit pass correcting drift between the tracked file and the
  actual repo state (stale commit references, contradictory Pages status, a phantom
  warning about SVG files that don't exist, undercounted `#reserve` asymmetry, and
  completed work still listed as pending).
- Sep 5, 2026: the client's negotiated agreement arrived signed and paid. This session
  reconciled the tracked files with what actually changed, then did the structural
  rebuild the agreement requires:
  - Phone number ownership resolved, service area confirmed, both recorded only in
    `PRIVATE_NOTES.local.md`
  - A client-sent design direction proposes different fonts and colors, explicitly not
    yet confirmed, flagged so nobody applies it prematurely
  - A signed commercial PDF was found sitting untracked in the repo root, one `git add`
    away from public exposure. Moved out, `.gitignore` hardened against a repeat
  - Domain is registered but resolves to the registrar's own page, not this repo,
    corrected in three places that previously undersold or mischaracterized this
  - `culture.html` renamed to `surgeons.html` via `git mv`, rebuilt to the agreement's
    spec: what OrthoFlow handles, what the office doesn't manage, a three-step referral
    process, coverage and response times, a compliance-note placeholder, and a new
    practice enquiry form. Vision, mission, and values moved into `about.html`
  - Nav, mobile menu, and footer updated across all three files, `#reserve` asymmetry
    reverified
  - The reserve form on `index.html` was found to violate the signed agreement's own
    field restrictions (a procedure-date field and a free-text notes field, neither
    allowed). Replaced the date field with the specified timing-range picklist and
    removed the free-text field. Added `.form-notice` to `styles.css` and the required
    medical-information notice to both forms
  - Corrected a mistaken claim written earlier in this same session, that `main.js`'s
    single-form handler would need updating for two forms. It does not: the two forms
    live on different pages, each with one form in its own DOM
  - The Patient Brokering Act compliance line was initially filed in
    `PRIVATE_NOTES.local.md`. Corrected: it's future public page copy pending attorney
    review, not a confidential detail, so it now lives in `CONTENT_DECK.md` instead
  - Later the same day: Sebby got registrar access and began wiring DNS. Both
    contact-detail gates (phone ownership, Elite Care business-listing verification)
    cleared, so the agreement's Section 2 holding page was built at the repo root, and
    the entire three-page build moved to `preview/` since GitHub Pages can only serve
    one `index.html` at the domain root. See "Two site areas" under Architecture.
    Relative asset paths and `og:url` tags fixed across all three moved files
  - The domain's DNS zone was confirmed by screenshot to carry live Microsoft 365
    business email and Teams/Skype for Business records well beyond what the DNS
    section had been warning about in the abstract. Documented the exact record set so
    a future session doesn't have to rediscover which of 20 records are safe to touch
  - None of this is committed yet, see `git status`
