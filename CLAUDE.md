# CLAUDE.md

Guidance for Claude Code. Read first, every session, before touching code.
See [CHANGELOG.md](CHANGELOG.md) for full session history.

---

## Bootstrap

**State as of 2026-09-12:** Agreement signed and paid. Three-page build lives under `preview/`; repo root `index.html` is the Section 2 holding page. DNS live. NICE1 assets wired. Homepage pricing section added.

```bash
git log --oneline -4 && git status --short
git fetch -q origin && git rev-list --left-right --count origin/main...main  # expect 0 0
curl -s -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com          # expect 200
curl -s -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com/preview/ # expect 200
```

| Area | State |
|---|---|
| Agreement | Signed 2026-09-04. Paid. Commercial terms in `PRIVATE_NOTES.local.md` only |
| Repo root `index.html` | Holding page only. NOT the homepage. See Architecture |
| `preview/` | Three-page build, all `[placeholder]` copy, all `noindex` |
| Fonts / colors | Client design direction proposed but NOT confirmed in writing. Do not touch `styles.css` |
| Enquiry forms | Wired: `mjyvjwlq` reserve, `xaeyaokw` practice. Not end-to-end tested |
| Business hours | Mon-Fri 8am-6pm confirmed. Sat/Sun not supplied |
| DNS / Pages | Fully live. A/AAAA resolve, HTTPS cert covers apex and `www` |

**Open decisions (ask Sebby, do not guess):** font/color confirmation, Sat/Sun hours, sibling client positioning.

**Client privacy:** contact details, commercial terms, and private client documents go in `PRIVATE_NOTES.local.md` (gitignored) only. Client address never published; use service area. No testimonials or patient videos without per-patient written authorization. Neither form may collect PHI.

**If a task would make this site look or read like Elite Care Recovery, stop and raise it.** See Hard Separation below.

---

## Hard Separation from Elite Care Recovery

- Never copy Elite Care prose, their `CONTENT_DECK.md`, Formspree ID `xeedwqvp`, phone numbers, or `@elitecarerecovery.net` addresses. Ortho Flow IDs: `mjyvjwlq` reserve, `xaeyaokw` practice (John's account).
- Never lift NICE product images from another dealer's site.
- Distinct color palette and type treatment, always. Signed contractual commitment (Section 11).
- No links between the two sites without both clients' written agreement. Signed term.

---

## Tech Stack: LOCKED

Plain HTML5 + CSS3 + vanilla JS. No build step, no npm, no bundler, no framework. Single `styles.css`, single `main.js`. Google Fonts via `<link>` (Playfair Display + Inter; client proposed Poppins + Source Sans 3, not confirmed, do not swap). Inline SVG icons only. Formspree free tier.

---

## Commands

Run all three sweeps before every commit touching markup.

```bash
python3 -m http.server 8000

# 1. Shared-chrome drift (preview/ only; holding page has no nav/footer).
#    Expect exactly THREE diffs per subpage: the intended #reserve asymmetry.
cd preview
for block in nav footer; do
  for page in about surgeons; do
    diff <(sed -n "/<$block>/,/<\/$block>/p" index.html) <(sed -n "/<$block>/,/<\/$block>/p" $page.html)
  done
done
for page in about surgeons; do
  diff <(sed -n '/<div class="mobile-menu">/,/<main/p' index.html) <(sed -n '/<div class="mobile-menu">/,/<main/p' $page.html)
done
cd ..

# 2. Em dash sweep. Must print nothing. Use `command grep` (plain grep is a ugrep
#    wrapper respecting .gitignore, which silently skips PRIVATE_NOTES.local.md).
LC_ALL=C command grep -rn $'\xe2\x80\x94' --include='*.html' --include='*.css' --include='*.js' --include='*.md' .

# 3. Pre-launch readiness (preview/ only). Must be zero before launch.
grep -rc '\[.*placeholder\|TODO\|REPLACE_WITH' preview/index.html preview/about.html preview/surgeons.html styles.css
```

```bash
# Verify #reserve links (sweep 1 catches only 2 of 4 per subpage)
grep -n 'href="index.html#reserve"' preview/about.html preview/surgeons.html  # expect 4 per file
grep -n 'href="#reserve"' preview/index.html                                   # expect 4
```

---

## Architecture

Three flat pages under `preview/` sharing root `styles.css` and `main.js` (via `../`), plus a standalone holding page at the repo root. No templating, no build step.

**Two site areas:** Root `index.html` is the holding page (logo, phone, service area, no nav/footer, not `noindex`). The marketing site is `preview/index.html`, `preview/about.html`, `preview/surgeons.html` (all `noindex`). At launch, promote `preview/`'s three files to repo root and retire the holding page in one pass.

**Page 3 (`surgeons.html`):** Audience is surgeons, practice managers, coordinators, ASC/discharge staff. Compliance-note section requires a healthcare attorney's review before any wording goes in. No referral-incentive language anywhere on this page.

**Enquiry forms (Section 5.3 of signed agreement):**
- Reserve form fields: name, phone, email, timing-range `<select>` only ("within 2 weeks", "2 to 6 weeks", "6 or more weeks", "not sure yet").
- Practice form fields: name, phone, email only.
- Never add: free-text medical field, surgery date, symptom/diagnosis, insurance, or any field that reveals a health event about a named person.
- Both show `.form-notice`: "Please do not include medical information in this form. We will contact you to discuss any specifics by phone."
- Formspree: `mjyvjwlq` reserve, `xaeyaokw` practice (John's own account). First submission may require John to confirm a Formspree activation email.

**Nav, mobile menu, footer** are copy-pasted across all three `preview/` pages. Changes must be made three times. The only intended divergence: subpages use `index.html#reserve` in four places (nav CTA, mobile-menu CTA, bottom CTA band, footer link); homepage uses `#reserve`. Sweep 1 catches only two of these; use the grep above for the other two.

`.mobile-menu` is outside `<nav>` on purpose. A positioned ancestor traps the fixed overlay.

**`main.js` gotchas:**
1. Fade-in CSS is injected at runtime (`main.js` appends a `<style>` with `.fade-out`/`.fade-in`/`@keyframes fadeInUp`). Not in `styles.css`. A section that never intersects stays invisible.
2. Form handler binds `document.querySelector('form')` (first form only). Safe because each page has exactly one form. Would break if a second form landed on the same page.
3. `setActiveNavLink()` only touches `.nav-links a`. Mobile menu links never get `.active`.

**Color tokens:** `--color-accent` / `--color-accent-dark` (not `--color-blue`). Section backgrounds are class-driven (`bg-cream`, `bg-cream-alt`, `bg-charcoal`, `bg-accent`). Do not change tokens on the design-direction document alone. Sky blue `#5DA0E2` is decorative only (fails WCAG AA): never text or buttons.

**Hero:** `.hero` has `background-color: var(--color-charcoal)` because text is white. Layer media on top; do not remove the background. Per-day rental rate must never publish alone; always show all tiers.

---

## DNS and Deploy

GitHub Pages live at `orthoflowrecovery.com`. Build type: `legacy` (Jekyll). DNS fully wired.

**This domain carries live Microsoft 365 email and Teams records. Never touch MX, either TXT record, or `_dmarc`.** Records to never touch: three MX to `*.ppe-hosted.com`, SPF TXT, `NETORGFT20691954.onmicrosoft.com` TXT, `TXT _dmarc` (`p=quarantine`), CNAMEs for `autodiscover`/`email`/`lyncdiscover`/`msoid`/`sip`, two SRV for Teams.

GitHub Pages IPs (apex needs all 8 or the cert silently never issues):
```
A     185.199.108.153  109.153  110.153  111.153
AAAA  2606:50c0:8000::153  8001::153  8002::153  8003::153
```

```bash
gh api repos/SebbyServices/OrthoFlowRecovery/pages --jq '{status,cname,build_type,html_url}'
dig +short orthoflowrecovery.com MX          # must be unchanged: 3x *.ppe-hosted.com
dig +short orthoflowrecovery.com TXT         # must show SPF and onmicrosoft.com
dig +short _dmarc.orthoflowrecovery.com TXT  # must show p=quarantine
```

---

## Behavioral Rules

1. **Stay in the lane.** Three pages, two forms.
2. **No copy invention.** All prose comes from approved `CONTENT_DECK.md`. No plausible-sounding copy, pricing, or stats. Signed agreement also prohibits implying operating history or patient counts the company does not have.
3. **No clinical claims.** Device language must be lifted verbatim from NICE-cleared language only.
4. **No referral incentive language** on the surgeons page.
5. **Premium over clever.** Editorial typography, generous whitespace, restrained color, gold used sparingly. No gradients, neon, glassmorphism.
6. **Contrast and readability.** Body text minimum 17px. Check any new color for WCAG AA before use.
7. **Accessibility is table stakes.** Semantic HTML, descriptive alt text, ARIA on icon-only buttons, visible focus states, skip link, labels tied to inputs.
8. **Image placeholders, not broken tags.** Use `.image-placeholder`. Never an external placeholder service.
9. **Mobile-first.** Min-width queries at 640/768/1024/1280. Touch targets 44x44px.
10. **Keep JS minimal.** No tracking, analytics, or third-party scripts beyond Google Fonts without explicit approval. Signed contractual term.
11. **No em dashes anywhere.** Use a colon for headings and definition lines; a full stop where the next clause stands alone. A blind comma swap creates comma splices.

---

## Open Items Before Launch

- [ ] Promote `preview/` three files to repo root; retire holding page
- [ ] Font and color confirmation from client in writing
- [ ] Healthcare attorney review of page 3 compliance line
- [ ] Client sign-off on `CONTENT_DECK.md` copy, then move into HTML
- [ ] Pricing figures for homepage pricing section (in writing)
- [ ] Resolve every `[FACT NEEDED]` in the content deck
- [ ] Sat/Sun business hours
- [ ] End-to-end test both Formspree forms (John may need to confirm first submission)
- [ ] Hero photo or video
- [ ] Social handles, then restore footer social icons
- [ ] Confirm NICE logo use, photography, and claims requirements
- [ ] Official reversed logo from client's designer
- [ ] **Remove `noindex, nofollow` from all three `preview/` pages at launch**

---

## This Repo Is Public

Every tracked file is readable on GitHub. `_config.yml` keeps internal docs off the live site but not off GitHub. If the build type ever changes from `legacy` to GitHub Actions, `_config.yml` stops being honored: re-run `curl -o /dev/null -w '%{http_code}\n' https://sebbyservices.github.io/OrthoFlowRecovery/CLAUDE.md` (expect 404) after any Pages change.

Never save a contract, invoice, or proposal into this folder. `.gitignore` excludes `*.pdf` and `*.docx`. All private content goes in `PRIVATE_NOTES.local.md` only.

---

## Logo Assets

| File | Use |
|---|---|
| `assets/ortho-flow-wordmark.png` | nav, mobile menu |
| `assets/ortho-flow-logo.png` | og:image, light backgrounds |
| `assets/ortho-flow-logo-reverse.png` | footer |
| `assets/ortho-flow-icon.png`, `favicon.png` | favicon, square uses |
| `assets/ortho-flow-logo-master.png` | source of truth (excluded from live site) |

All five are client-owned per the signed agreement. Master is 960x640 raster: fine for web, not print. The reversed logo was recolored here; ask the client's designer for an official version before launch.
