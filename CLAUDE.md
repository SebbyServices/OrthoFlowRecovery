# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Read this file first, every session, before touching code.

---

## START HERE: Session Bootstrap

**Last session: 2026-08-26.** Skeleton pushed, GitHub Pages now **live** at
`https://sebbyservices.github.io/OrthoFlowRecovery/` with no custom domain attached.
The client sent the logo and his contact details on 2026-08-26. Brand colors and logo
assets are now real. Copy is still all placeholder.

**Contact details are supplied but NOT publishable yet.** There is an unresolved
conflict over which phone number belongs to this business. Details, deliberately kept
out of this tracked file, are in `PRIVATE_NOTES.local.md`.

### 1. Orient (run these first, in order)

```bash
git log --oneline -4          # expect 4c589b5, 91f15f8, 7d35367, cfcdb98
git status --short            # expect clean
git fetch -q origin && git rev-list --left-right --count origin/main...main   # expect 0 0
python3 -m http.server 8000   # preview at http://localhost:8000
```

### 2. Where things actually stand

| Area | State |
|---|---|
| Page structure (3 pages) | Built, well-formed, verified |
| `styles.css` / `main.js` | Ported and working |
| Nav / mobile menu / footer | Built, identical across all three pages except the intended `index.html#reserve` asymmetry |
| Client copy | **None.** Every headline and paragraph is `[placeholder]` |
| Logo / favicon | **Real.** Client logo received 2026-08-26, web assets derived |
| Brand color | **Real.** Navy `#003677`, sky `#5DA0E2` decorative only, gray `#5C646F` |
| Contact phone / email / hours | Supplied but withheld, see `PRIVATE_NOTES.local.md`. Hours unknown |
| Formspree form | **Deliberately unwired**, `REPLACE_WITH_ORTHO_FLOW_FORM_ID` |
| Product / device line | **NICE, confirmed.** Exact model still unconfirmed |
| Domain / DNS / Pages | Pages LIVE on `github.io`. Domain exists but is NOT wired, no `CNAME` |
| Pushed to GitHub | Yes, `4c589b5` on public `main` |

### 3. Ask Sebby before doing anything else

These are open decisions, not tasks. Do not resolve them by guessing.

1. **Is this paid from day one?** Elite Care was a free demo that was meant to convert.
   Sebby has not said which model applies here.
2. **The unresolved contact detail conflict.** Highest priority, blocks the footer.
3. **Positioning against the sibling client**, now that the device line overlaps.
4. **The real service area**, which may not be the one currently in the markup.
5. **Whether the client supplied testimonials are usable.** Default answer is no.

All four are written up in `PRIVATE_NOTES.local.md`. They are kept out of this file
on purpose because this file is public. Read that file before acting on any of them.

### 3b. Client supplied material: handle in the private notes

Two things arrived from the client on 2026-08-26 that cannot be summarized in a tracked
file: a contact detail conflict, and a document the client marked private that contains
identifiable patient health information. Both are written up in
`PRIVATE_NOTES.local.md`.

The operative rules here, which are safe to state publicly:

- The phone number in the HTML stays a placeholder until the conflict is resolved.
- No client supplied testimonial, quote, or patient video goes on this site. Not
  paraphrased, not anonymized by first name alone. The default is no, and changing that
  needs written per patient marketing authorization and a legal read, not a judgment
  call made here.
- Do not restate the contents of the private document in any tracked file, commit
  message, or comment.

### 4. Work that is UNBLOCKED right now

Safe to do without any client input:

- Responsive QA at 375px, 768px, 1280px on all three pages
- Keyboard-only tab pass, confirm focus states are visible
- Confirm no section is stuck at `opacity: 0` (see the fade-in note below)
- Lighthouse pass on structure and accessibility
- Tighten semantics or ARIA where the ported markup is weak
- Promote the lead `<h2>` on `about.html` and `culture.html` to `<h1>`. Only
  `index.html` has an `<h1>` today, so both subpages ship with no top-level heading.
  This is a markup fix, not a copy change, so it needs no client input

### 5. Work that is BLOCKED on the client

Do not start these, and do not invent content to unblock them:

- Any real copy. It goes in `CONTENT_DECK.md` first, then into the HTML
- Logo, favicon, brand colors
- Phone, email, business hours, service area specifics
- Formspree form creation and ID
- Hero photo or video
- Domain, DNS, GitHub Pages, `CNAME`

### 6. Standing rule for this repo

If a task would make this site read or look like Elite Care Recovery, stop and raise it.
See "Hard Separation" below. That section is the most important part of this file.

---

## Project Snapshot

- **Client:** Ortho Flow Recovery (Miami, FL)
- **Business:** Post-operative recovery equipment, serving Miami and surrounding areas
- **Owner contact:** see `PRIVATE_NOTES.local.md`
- **Domain:** `orthoflowrecovery.com` (NOT yet wired to this repo, see DNS section)
- **Repo:** `github.com/SebbyServices/OrthoFlowRecovery`, **public**
- **Developer:** Sebby IT Consulting, Corp.
- **Status:** Live on GitHub Pages with real brand assets and no approved copy. See
  "START HERE" above for the current state.

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
  Care's inbox. Ortho Flow needs its own form. The placeholder in `index.html` is
  `REPLACE_WITH_ORTHO_FLOW_FORM_ID`.
- **Never reuse the Elite Care phone number** or any `@elitecarerecovery.net` address.
  The specific numbers live in `PRIVATE_NOTES.local.md`, which is gitignored. Do not
  write client contact details into any tracked file. See "This repo is public" below.
- **Never copy Elite Care or NICE product assets.** Confirmed 2026-08-26: the NICE1 is a
  manufacturer product sold through a national dealer network, not Elite Care's
  exclusive line. Neu Medical DME in Minnesota sells the same device, and so does the
  sibling client, so the two sites cannot differentiate on hardware at all.
  Differentiation has to come from service, delivery, and support.
  Product photography still belongs to NICE or to whichever dealer commissioned it.
  Never lift product images from another dealer's site. Ask whether NICE publishes an
  authorized dealer asset kit instead.
- **Never copy `CONTENT_DECK.md` from the Elite Care repo.** That is their approved
  client content.

If a change would make the two sites look or read alike, stop and raise it.

---

## Tech Stack: LOCKED

Same rationale as the Elite Care build: non-technical client, static hosting, handoff
must be readable by any web dev.

- Plain HTML5 + CSS3 + vanilla JS
- No build step, no npm, no bundler, no framework
- Single `styles.css`, single `main.js`
- Google Fonts via `<link>` (Playfair Display + Inter)
- Inline SVG icons only
- Form: Formspree (free tier), ID not yet provisioned

---

## Commands

There is no build, no lint, and no test runner. These are the checks that stand in for
them. Run the three sweeps before every commit that touches markup.

```bash
# Serve locally, then open http://localhost:8000. No build step, just refresh.
python3 -m http.server 8000

# 1. Shared-chrome drift. All three files must match, and the ONLY expected diff is
#    the intended `index.html#reserve` asymmetry described under Architecture.
for block in nav footer; do
  for page in about culture; do
    echo "== $block: index vs $page =="
    diff <(sed -n "/<$block>/,/<\/$block>/p" index.html) \
         <(sed -n "/<$block>/,/<\/$block>/p" $page.html)
  done
done
diff <(sed -n '/<div class="mobile-menu">/,/<main/p' index.html) \
     <(sed -n '/<div class="mobile-menu">/,/<main/p' about.html)

# 2. Em dash sweep. Rule 9 below. Must print nothing.
LC_ALL=C grep -rn $'\xe2\x80\x94' --include='*.html' --include='*.css' --include='*.js' --include='*.md' .

# 3. Pre-launch readiness. Roughly 87 hits today, MUST be zero before launch. The
#    pattern deliberately skips the legitimate `.image-placeholder` class.
grep -rc '\[.*placeholder\|TODO\|REPLACE_WITH' index.html about.html culture.html styles.css
```

---

## Architecture

Three flat HTML pages sharing one stylesheet and one script.

### The nav, mobile menu, and footer are copy-pasted into all three pages

There is no templating. Any change to `<nav>`, `.mobile-menu`, or `<footer>` must be
applied **three times**. This was the #1 regression source on the Elite Care build.
Verify with:

```bash
diff <(sed -n '/<nav>/,/<\/nav>/p' index.html) <(sed -n '/<nav>/,/<\/nav>/p' about.html)
```

See "Commands" above for the full three-file sweep across nav, mobile menu, and footer.

The only **intended** divergence: the reserve form lives on the homepage, so subpages
link `index.html#reserve` where the homepage links `#reserve`. This happens in **three**
places per subpage, and all three are easy to miss: the nav CTA, the mobile menu CTA,
and the footer quick link. Preserve that asymmetry. Making them identical breaks the
subpage CTAs.

### `.mobile-menu` sits outside `<nav>` on purpose

A positioned ancestor traps the fixed overlay. Do not move it back inside `<nav>`.

### Section backgrounds are class-driven, never inline

| Class | Effect |
|---|---|
| `section.bg-cream` | `--color-bg` |
| `section.bg-cream-alt` | `--color-bg-alt` |
| `section.bg-charcoal` | charcoal bg, white text, gold eyebrows |
| `section.bg-accent` | accent bg, white text. Bottom CTA bands on About/Culture |

Note the token rename from the Elite Care build: `--color-blue` is `--color-accent`
here, and `.bg-blue` is `.bg-accent`, because Ortho Flow's brand color is unknown.

**The placeholder teal is hardcoded in three files, not one.** `--color-accent` and
`--color-accent-dark` in `styles.css`, the bar in `assets/ortho-flow-logo.svg`, and the
tile in `favicon.svg` all carry `#0F766E` literally. Swapping only the CSS token leaves
two teal assets on a rebranded site.

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
fade-in, plus `setActiveNavLink()`.

Three things that surprise people:

1. **The fade-in CSS is injected at runtime.** `main.js` appends a `<style>` block
   defining `.fade-out` / `.fade-in` / `@keyframes fadeInUp`. Searching `styles.css`
   finds nothing. Every `section`, `.card`, and `.step-card` starts at `.fade-out`, so
   **a section that never intersects stays invisible**.
2. **The form handler binds `document.querySelector('form')`**, the first form on the
   page only. A second form gets no JS enhancement. It also `preventDefault()`s
   unconditionally, so while the Formspree ID is still
   `REPLACE_WITH_ORTHO_FLOW_FORM_ID` every submit lands in the catch branch and shows
   the error state. That is the expected behavior right now, not a bug to chase.
3. **`setActiveNavLink()` only touches `.nav-links a`.** The `.mobile-menu` links never
   receive `.active`, so the mobile overlay shows no current-page indicator.

### `.hero` carries an explicit background

There is no hero media yet and the hero text is white. `.hero` sets
`background-color: var(--color-charcoal)` for that reason. Do not remove it when adding
media, layer the media on top.

---

## DNS and Deploy: read before touching the domain

GitHub Pages is **not yet enabled** on this repo and there is deliberately **no `CNAME`
file**. Both were left out on purpose.

Lessons carried over from the Elite Care launch, which cost four days:

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
3. **Clear any registrar domain forwarding first.** A GoDaddy forwarding rule injects
   foreign A records that break domain validation.
4. **Do not enable Enforce HTTPS until the certificate covers every hostname you serve.**
5. **If the domain carries business email, never touch MX, SPF, DKIM, or DMARC** while
   doing website DNS. Verify them before and after every change.

Verify with:

```bash
# once the domain is wired, all four of these must look right before enabling HTTPS
dig +short orthoflowrecovery.com A
dig +short orthoflowrecovery.com AAAA        # the one that stalled Elite Care
dig +short orthoflowrecovery.com MX          # confirm business email is untouched
gh api repos/SebbyServices/OrthoFlowRecovery/pages --jq '.https_certificate.domains'
```

Note: `gh api .../pages` returns 404 until GitHub Pages is enabled on the repo. That is
expected right now, not an error.

---

## Behavioral Rules

1. **Stay in the lane.** v1 is a marketing brochure site. Three pages, one form.
2. **No copy invention.** All client-facing prose comes from an approved
   `CONTENT_DECK.md`. Until that file has real content, placeholders stay placeholders.
   Do not write plausible-sounding marketing copy to fill gaps.
3. **Premium over clever.** White-glove medical service brand. Editorial typography,
   generous whitespace, restrained color, gold used sparingly. No gradients, neon,
   glassmorphism, or trend-chasing UI.
4. **Contrast and readability are non-negotiable.** Audience skews 50+ post-op patients.
   Always set background and text color explicitly. Body text 17px.
5. **Accessibility is table stakes.** Semantic HTML, descriptive alt text, ARIA labels on
   icon-only buttons, visible focus states, skip link, labels tied to inputs.
6. **Image placeholders, not broken tags.** Use `.image-placeholder`. Never an external
   placeholder service.
7. **Mobile-first.** Min-width queries at 640/768/1024/1280. Touch targets 44x44px.
8. **Keep JS minimal.** No tracking, no analytics, no third-party scripts beyond Google
   Fonts without explicit approval.
9. **No em dashes anywhere.** Not in copy, comments, commit messages, or docs. Use a
   comma, a colon, or a full stop. When replacing one, a blind swap to a comma creates
   comma splices, so use a colon for headings and definition-style lines and a full stop
   where the next clause stands alone. Five em dashes came across in the ported
   `styles.css` and `main.js` comments and were cleaned on 2026-08-25. Re-check after
   porting anything else from another repo.

---

## Open Items Before This Can Launch

- [ ] Approved copy for all three pages (`CONTENT_DECK.md` is an empty template)
- [x] Ortho Flow logo received 2026-08-26, web assets derived and wired in
- [x] Brand colors sampled from the logo and written into `styles.css`
- [x] Device line confirmed as NICE. Exact model still open
- [ ] Resolve the phone number collision before publishing any contact details
- [ ] Confirm the real service area, Miami vs Palm Beach
- [ ] Business phone, contact email, real business hours, service area
- [ ] Create the Ortho Flow Formspree form and wire the real ID
- [ ] Hero photo or video
- [ ] Social handles
- [ ] Domain purchase, DNS, GitHub Pages, then `CNAME`
- [ ] Decide whether this is a paid engagement from the start

---

## Testing Checklist

- [ ] 375px, 768px, 1280px on all three pages, no horizontal scroll
- [ ] Nav / mobile menu / footer edits landed in **all three** files
- [ ] Subpages use `index.html#reserve` in all three spots (nav CTA, mobile menu CTA,
      footer quick link), homepage uses `#reserve`
- [ ] Every page has exactly one `<h1>`
- [ ] Sections alternate `.bg-cream` / `.bg-cream-alt` correctly
- [ ] Scroll every page fully, nothing stuck at `opacity: 0`
- [ ] Keyboard-only tab pass, focus states visible
- [ ] No console errors
- [ ] No remaining `[placeholder]`, `TODO`, or `REPLACE_WITH` text before launch
- [ ] No dead anchors. `index.html` currently ships four: `href="tel:"`,
      `href="mailto:"`, and two social `href="#"`. They will fail an a11y pass, and
      each one unblocks only when the client supplies the phone, email, or handles
- [ ] Brand color swapped in all three places: `styles.css`, the logo SVG, the favicon
- [ ] Lighthouse: Performance 90+, Accessibility 95+, Best Practices 95+

---

## This repo is public, and so is everything Pages serves

The repo is public **and** GitHub Pages serves the repository root, which means every
tracked file is fetchable at the live site URL, not just the HTML. Internal notes are
excluded from the published site by `_config.yml`, but exclusion is not secrecy: the
files are still readable on GitHub itself.

So the rule is simple. **Client contact details, commercial terms, cross client notes,
and anything from a document a client marked private go in `PRIVATE_NOTES.local.md`,
which is gitignored.** Never in `CLAUDE.md`, `CONTENT_DECK.md`, `README.md`, an HTML
comment, or a commit message.

---

## Logo assets

The client sent one file, a 4096x2730 stacked PNG. The nav slot was built for a
horizontal wordmark at roughly 5.3:1, and the supplied lockup is 1.5:1, so dropping it
straight in would have wrecked the nav. Four derived assets are committed instead:

| File | Use | Notes |
|---|---|---|
| `assets/ortho-flow-wordmark.png` | nav, mobile menu | "OrthoFlow RECOVERY" only, 4:1, no icon |
| `assets/ortho-flow-logo.png` | og:image, light backgrounds | full stacked lockup |
| `assets/ortho-flow-logo-reverse.png` | footer | navy recolored to white for the charcoal footer |
| `assets/ortho-flow-icon.png`, `favicon.png` | favicon, square uses | the circle mark alone |
| `assets/ortho-flow-logo-master.png` | source of truth | 2048px, regenerate the others from this |

The reversed lockup was produced here by recoloring, not supplied by the client. Ask
John whether his designer has an official reversed version before launch.

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
- Aug 25, 2026: pushed to the public remote at Sebby's go-ahead. Bootstrap state table,
  orientation commands, and the open-decisions list updated to match.
- Aug 26, 2026: client sent the logo and contact details. Brand tokens replaced with the
  real navy `#003677`, logo assets derived and wired across all three pages, favicon
  swapped to PNG, `noindex` added while the live site still shows placeholder copy.
  Device line confirmed as NICE. Logged the phone number collision and the patient
  testimonial compliance block as the two things now gating contact details and social
  proof. Enabled Pages, no custom domain.
- Aug 26, 2026: `/init` audit pass. Corrected the bootstrap state, which still pointed
  at `91f15f8` and claimed the work was unpushed. Added a "Commands" section holding the
  three sweeps that stand in for a build and test suite. Recorded that the `index.html`
  vs subpage `#reserve` asymmetry appears in three places per subpage, not two, that the
  placeholder teal is hardcoded in `styles.css`, the logo SVG, and the favicon, and that
  `about.html` and `culture.html` currently have no `<h1>`.
