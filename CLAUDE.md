# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Read this file first, every session, before touching code.

See CHANGELOG.md for session history.

---

## START HERE: Session Bootstrap

**Last session: 2026-09-12.** Agreement signed and paid. Full three-page build is under
`preview/`; repo root `index.html` is the Section 2 holding page. DNS is live. Most
recent commits added the NICE1 assets and homepage pricing section.

**Repo root `index.html`** is the holding page (logo, phone, service area, "Now Taking
Reservations"), not the site homepage. The three-page marketing site is at `preview/`.
All content under `preview/` is still `[placeholder]`; every page there carries `noindex`.

### 1. Orient (run these first, in order)

```bash
git log --oneline -4
git status --short
git fetch -q origin && git rev-list --left-right --count origin/main...main  # expect 0 0
python3 -m http.server 8000   # holding page at :8000/, full build at :8000/preview/
curl -s -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com          # expect 200
curl -s -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com/preview/ # expect 200
```

### 2. Current state

| Area | State |
|---|---|
| Agreement | Signed 2026-09-04. Paid. Commercial terms in `PRIVATE_NOTES.local.md` only |
| Repo root `index.html` | Holding page. Not the homepage. See "Two site areas" |
| `preview/` | Three-page marketing site, all `[placeholder]` copy, all `noindex` |
| Page 3 (`surgeons.html`) | Sections scaffolded, no real copy |
| Fonts / colors | Client design direction proposed but NOT confirmed in writing. Do not touch `styles.css` |
| Enquiry forms | Both field-restricted, both wired: `mjyvjwlq` reserve, `xaeyaokw` practice. Not end-to-end tested |
| Business hours | Mon-Fri 8am-6pm confirmed. Sat/Sun not supplied |
| DNS / Pages | Live. A/AAAA resolve, HTTPS cert covers apex and `www`, both URLs return 200 |
| NICE1 assets | Wired on homepage as of 2026-09-12 |
| Homepage pricing | Added 2026-09-12 with John's confirmed facts |

### 3. Open decisions (ask Sebby, do not guess)

1. **Font and color confirmation.** Proposed but not confirmed in writing. Do not touch `styles.css` typography or color tokens.
2. **Sat/Sun business hours.** Not yet supplied.
3. **Positioning against the sibling client** beyond the signed structural constraints. Details in `PRIVATE_NOTES.local.md`.

### 4. Client supplied material

Contact details, commercial terms, and anything from a private client document go in `PRIVATE_NOTES.local.md` (gitignored). Never in any tracked file, commit message, or comment. The client's address is never published; use the service area instead. No testimonials or patient videos without written per-patient marketing authorization. Neither form may collect PHI (free-text medical info, surgery date, diagnosis, insurance) per the signed agreement.

### 5. UNBLOCKED right now

- Responsive QA at 375px, 768px, 1280px on all three `preview/` pages
- Keyboard-only tab pass, confirm focus states visible
- Confirm no section is stuck at `opacity: 0` (see JS notes under Architecture)
- Lighthouse pass on structure and accessibility
- Tighten semantics or ARIA where ported markup is weak
- Structural work on `preview/surgeons.html` and form markup, no real copy or compliance wording

### 6. BLOCKED

- Any real copy for any `preview/` page. Client approves it in `CONTENT_DECK.md` line by line first
- Publishing the client's street address
- Sat/Sun hours
- Hero photo or video
- Any `styles.css` font or color change, pending written confirmation
- The Patient Brokering Act compliance line on page 3, without a healthcare attorney's review
- Social handles (footer social icons are commented out for this reason)

### 7. Standing rule

If a task would make this site read or look like Elite Care Recovery, stop and raise it. See "Hard Separation" below. This is a signed contractual commitment.

---

## Hard Separation from Elite Care Recovery

This skeleton borrowed Elite Care's **architecture and design system only**. Everything below is forbidden to carry across:

- **Never copy Elite Care prose, `CONTENT_DECK.md`, the Formspree ID `xeedwqvp`, phone numbers, or `@elitecarerecovery.net` addresses.** Ortho Flow's Formspree IDs: `mjyvjwlq` reserve, `xaeyaokw` practice (John's account).
- **Never lift NICE product images from another dealer's site.** The NICE1 ships through a national dealer network; ask NICE for an authorized asset kit.
- **Distinct color palette and type treatment, always.** Signed contractual commitment (Section 11). If the pending design direction converges visually with Elite Care, raise it.
- **No links between the two sites** without both clients' written agreement. Signed term.

If a change would make the two sites look or read alike, stop and raise it.

---

## Tech Stack: LOCKED

- Plain HTML5 + CSS3 + vanilla JS
- No build step, no npm, no bundler, no framework
- Single `styles.css`, single `main.js`
- Google Fonts via `<link>`, currently Playfair Display + Inter. A client design direction proposes Poppins + Source Sans 3: **not confirmed in writing, do not swap**
- Inline SVG icons only
- Formspree (free tier): `mjyvjwlq` reserve, `xaeyaokw` practice

---

## Commands

No build, no lint, no test runner. Run all three sweeps before every commit that touches markup.

```bash
# Serve locally
python3 -m http.server 8000

# 1. Shared-chrome drift within preview/ only (holding page has no nav/footer).
#    Expect exactly THREE diffs per subpage: the intended index.html#reserve asymmetry
#    (one in nav, one in mobile-menu, one in footer). Anything else is real drift.
cd preview
for block in nav footer; do
  for page in about surgeons; do
    echo "== $block: index vs $page =="
    diff <(sed -n "/<$block>/,/<\/$block>/p" index.html) \
         <(sed -n "/<$block>/,/<\/$block>/p" $page.html)
  done
done
for page in about surgeons; do
  echo "== mobile-menu: index vs $page =="
  diff <(sed -n '/<div class="mobile-menu">/,/<main/p' index.html) \
       <(sed -n '/<div class="mobile-menu">/,/<main/p' $page.html)
done
cd ..

# 2. Em dash sweep, whole repo including PRIVATE_NOTES.local.md. Must print nothing.
#    Use `command grep`, not plain `grep` (grep is a ugrep wrapper that respects
#    .gitignore, silently skipping PRIVATE_NOTES.local.md and giving a false pass).
LC_ALL=C command grep -rn $'\xe2\x80\x94' --include='*.html' --include='*.css' --include='*.js' --include='*.md' .

# 3. Pre-launch readiness, preview/ only. Must be zero before launch.
#    (Skips the legitimate .image-placeholder class; excludes the holding page on purpose.)
grep -rc '\[.*placeholder\|TODO\|REPLACE_WITH' preview/index.html preview/about.html preview/surgeons.html styles.css
```

Verify the four `#reserve` links per subpage (sweep 1 catches only two of them):

```bash
grep -n 'href="index.html#reserve"' preview/about.html preview/surgeons.html  # expect 4 per file
grep -n 'href="#reserve"' preview/index.html                                   # expect 4
```

---

## Architecture

Three flat HTML pages sharing one stylesheet and one script, plus a standalone holding page at the repo root.

### Two site areas

GitHub Pages can only serve one `index.html` at the domain root:

- **Repo root `index.html`**: the Section 2 holding page. Logo, phone, service area, "Now Taking Reservations." No nav, no footer. Shares `styles.css` for tokens/fonts only plus a small scoped inline `<style>`. Deliberately **not** `noindex`. Overwritten entirely at launch.
- **`preview/`**: the actual three-page marketing site (`preview/index.html`, `preview/about.html`, `preview/surgeons.html`). Shares root `styles.css` and `main.js` via `../`. All pages carry `noindex`. Not linked from the holding page.

**At launch:** promote `preview/`'s three files back to the repo root and retire the holding page as one deliberate pass. Re-run every sweep with paths restored to root.

### Page 3: `surgeons.html`

Audience is surgeons, practice managers, surgical coordinators, ASC/discharge staff. Sections: what OrthoFlow handles, what the referring office doesn't manage, a three-step "how to refer" row, coverage and response times, compliance-note placeholder, practice enquiry form.

**The compliance-note section requires a healthcare attorney's review before any wording goes in.** Do not draft referral-incentive language anywhere on this page.

### Enquiry forms

Both forms are field-restricted by the signed agreement (Section 5.3):

- **Allowed fields:** name, phone, email, and on the reserve form only a timing-range picklist (`<select>`: "within 2 weeks", "2 to 6 weeks", "6 or more weeks", "not sure yet").
- **Never add:** free-text medical field, surgery/procedure date, symptom or diagnosis field, insurance field, or anything that would reveal a health event about a named person.
- Both show the required notice (`.form-notice`): "Please do not include medical information in this form. We will contact you to discuss any specifics by phone."
- Formspree IDs: `mjyvjwlq` reserve, `xaeyaokw` practice (John's own account). Not yet tested end-to-end. Formspree commonly requires confirming a brand-new form on its first submission (confirmation email to the account owner).

Adding a PHI-capable field is out of scope and requires a separate written change order.

### Nav, mobile menu, and footer

Copy-pasted into all three `preview/` pages. Any change must be applied three times. This was the #1 regression source on the Elite Care build.

The only intended divergence: subpages link `index.html#reserve` where the homepage links `#reserve`. This happens in **four** places per subpage:

| # | Location | Caught by sweep 1? |
|---|---|---|
| 1 | nav CTA | yes |
| 2 | mobile menu CTA | no, `.mobile-menu` is outside `<nav>` |
| 3 | bottom CTA band button | no, it's page body |
| 4 | footer quick link | yes |

`.mobile-menu` sits outside `<nav>` on purpose: a positioned ancestor traps the fixed overlay.

### Section backgrounds and color tokens

Section backgrounds are class-driven (`section.bg-cream`, `.bg-cream-alt`, `.bg-charcoal`, `.bg-accent`). Token names use `--color-accent` / `--color-accent-dark` (not `--color-blue`). Keep neutral token names regardless of actual color values.

**Do not change color tokens** on the strength of the client's design-direction document alone. When written confirmation arrives, reconcile against `PRIVATE_NOTES.local.md`.

### `main.js`: three gotchas

1. **Fade-in CSS is injected at runtime.** `main.js` appends a `<style>` block with `.fade-out` / `.fade-in` / `@keyframes fadeInUp`. Nothing in `styles.css`. Every `section`, `.card`, and `.step-card` starts at `.fade-out`: a section that never intersects stays invisible.
2. **Form handler binds `document.querySelector('form')`**, the first form only. Safe now because the two forms live on different pages, each with one form in its DOM. Would break if a second form ever landed on the same page.
3. **`setActiveNavLink()` only touches `.nav-links a`.** Mobile menu links never receive `.active`.

The success message deliberately promises no response time. Do not add a time commitment without written client agreement.

### Hero and pricing notes

`.hero` has an explicit `background-color: var(--color-charcoal)` because the text is white and there is no hero media yet. Layer media on top; do not remove the background.

**A per-day rental rate must never publish alone.** Always show all tiers together.

---

## DNS and Deploy

GitHub Pages is live at `orthoflowrecovery.com`. Build type: `legacy` (Jekyll). DNS fully wired and verified.

**This domain carries live Microsoft 365 business email and Teams records. Never touch MX, either TXT record, or `_dmarc`.**

Zone breakdown (20 records total):
- **Website records (already set):** four A + four AAAA to GitHub Pages, `CNAME www` to `sebbyservices.github.io`.
- **Never touch:** three MX to `*.ppe-hosted.com`, SPF TXT, `NETORGFT20691954.onmicrosoft.com` TXT, `TXT _dmarc` (`p=quarantine`), CNAMEs for `autodiscover`/`email`/`lyncdiscover`/`msoid`/`sip`, two SRV for Teams.
- **Leave alone:** `CNAME pay`, `CNAME _domainconnect`, NS, SOA.

```bash
# Check Pages state
gh api repos/SebbyServices/OrthoFlowRecovery/pages --jq '{status,cname,build_type,html_url}'

# Verify DNS before and after any DNS edit
dig +short orthoflowrecovery.com A           # 4 GitHub IPs
dig +short orthoflowrecovery.com AAAA        # 4 GitHub IPv6s
dig +short orthoflowrecovery.com MX          # MUST be unchanged: 3x *.ppe-hosted.com
dig +short orthoflowrecovery.com TXT         # MUST show SPF and onmicrosoft.com string
dig +short _dmarc.orthoflowrecovery.com TXT  # MUST show p=quarantine
gh api repos/SebbyServices/OrthoFlowRecovery/pages --jq '.https_certificate.domains'
```

Hard-won lessons (see CHANGELOG.md for details):
1. Set the custom domain in ONE place (Pages settings or `CNAME` file), then `git pull`.
2. Apex domain needs four A records AND four AAAA records. Missing AAAA = certificate silently never issues.
   ```
   A     185.199.108.153  109.153  110.153  111.153
   AAAA  2606:50c0:8000::153  8001::153  8002::153  8003::153
   ```
3. Disconnect GoDaddy Website Builder before editing the `A` record (it's a managed pointer, not a plain IP).
4. Do not enable Enforce HTTPS until the certificate covers every hostname.

---

## Behavioral Rules

1. **Stay in the lane.** v1 is a marketing brochure: three pages, two forms.
2. **No copy invention.** All client-facing prose comes from approved `CONTENT_DECK.md`. Do not write plausible-sounding copy, pricing figures, or statistics. The signed agreement also prohibits implying operating history, patient counts, or years in business the company does not have.
3. **No clinical claims, ever.** Nothing may say the device reduces pain, swelling, or medication use. Any such wording must be lifted verbatim from NICE-cleared language.
4. **No referral incentive language, ever** on the surgeons and practices page.
5. **Premium over clever.** Editorial typography, generous whitespace, restrained color, gold used sparingly. No gradients, neon, glassmorphism, or trend-chasing UI.
6. **Contrast and readability.** Body text at least 17px. The sky blue `#5DA0E2` fails WCAG AA on cream and white: decorative only, never text or buttons. Check new color values before use.
7. **Accessibility is table stakes.** Semantic HTML, descriptive alt text, ARIA labels on icon-only buttons, visible focus states, skip link, labels tied to inputs.
8. **Image placeholders, not broken tags.** Use `.image-placeholder`. Never an external placeholder service.
9. **Mobile-first.** Min-width queries at 640/768/1024/1280. Touch targets 44x44px.
10. **Keep JS minimal.** No tracking, no analytics, no third-party scripts beyond Google Fonts without explicit approval. This is a signed contractual term.
11. **No em dashes anywhere.** Not in copy, comments, commit messages, or docs. Use a comma, colon, or full stop. A blind swap to a comma creates comma splices: use a colon for headings and definition-style lines, a full stop where the next clause stands alone.

---

## Open Items Before Launch

- [ ] Promote `preview/`'s three files to repo root and retire holding page
- [ ] Font and color confirmation from client, in writing
- [ ] Healthcare attorney review of page 3 referral-incentive compliance line
- [ ] Client sign-off on `CONTENT_DECK.md` draft copy, then move into HTML
- [ ] Pricing figures for homepage pricing section, supplied in writing
- [ ] Resolve every `[FACT NEEDED]` tag in the content deck
- [ ] Sat/Sun business hours
- [ ] End-to-end test both Formspree forms with a real submission (John may need to confirm first submission by email)
- [ ] Update `main.js` form handler if a second form ever lands on the same page
- [ ] Hero photo or video
- [ ] Social handles, then restore footer social icons
- [ ] Confirm NICE requirements for logo use, product photography, and claims
- [ ] Ask client's designer for official reversed logo
- [ ] **Remove `noindex, nofollow` from all three `preview/` pages at launch** (easy to forget)

---

## Testing Checklist

**Holding page:** renders at 375/768/1280px; `tel:` link is 44px+ tap target; no `noindex`; no pricing or clinical claims.

**`preview/` pages (all three):**
- [ ] No horizontal scroll at 375/768/1280px
- [ ] Nav / mobile menu / footer identical across all three files (except intended `#reserve` asymmetry)
- [ ] Subpages use `index.html#reserve` in all four spots; homepage uses `#reserve`
- [ ] One `<h1>` per page; sections alternate `.bg-cream` / `.bg-cream-alt`
- [ ] Scroll fully, nothing stuck at `opacity: 0`; keyboard-only tab pass; no console errors
- [ ] No `[placeholder]`, `TODO`, or `REPLACE_WITH` text (pre-launch)
- [ ] `noindex` removed from all three pages (pre-launch)
- [ ] Neither enquiry form has a PHI-capable field; both show the medical-information notice
- [ ] Pricing section never shows a per-day figure alone
- [ ] Lighthouse: Performance 90+, Accessibility 95+, Best Practices 95+

---

## This Repo Is Public

Every tracked file is readable on GitHub. `_config.yml` excludes internal docs from the live site, but not from GitHub itself. If the build type ever changes from `legacy` to a GitHub Actions workflow, `_config.yml` stops being honored: re-run `curl -o /dev/null -w '%{http_code}\n' https://sebbyservices.github.io/OrthoFlowRecovery/CLAUDE.md` (expect 404) after any Pages change.

**Never save a contract, invoice, or proposal into this folder.** `.gitignore` excludes `*.pdf` and `*.docx`. All private content goes in `PRIVATE_NOTES.local.md` only.

---

## Logo Assets

| File | Use |
|---|---|
| `assets/ortho-flow-wordmark.png` | nav, mobile menu (4:1 horizontal, no icon) |
| `assets/ortho-flow-logo.png` | og:image, light backgrounds |
| `assets/ortho-flow-logo-reverse.png` | footer (navy recolored to white) |
| `assets/ortho-flow-icon.png`, `favicon.png` | favicon, square uses |
| `assets/ortho-flow-logo-master.png` | source of truth (excluded from published site) |

All five are confirmed client-owned per the signed agreement. Master is a 960x640 raster: fine for web, not print. The reversed lockup was recolored here; ask the client's designer for an official version before launch.
