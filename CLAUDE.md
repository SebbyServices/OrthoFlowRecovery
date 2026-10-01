# CLAUDE.md

Guidance for Claude Code. Read first, every session, before touching code.
See [CHANGELOG.md](CHANGELOG.md) for full session history.

---

## Bootstrap

**State as of 2026-09-30:** Site launched 2026-09-22 (`ae071d1`). Three pages live at the repo root plus Spanish copies under `es/`, all indexable. Holding page retired. Legal pages live but still drafts. SMS terms and privacy pages live for Spruce carrier registration.

```bash
git log --oneline -4 && git status --short
git diff --cached --stat                                                      # expect empty: other sessions edit this tree
git fetch -q origin && git rev-list --left-right --count origin/main...main  # expect 0 0
for p in "" about.html surgeons.html es/ es/about.html es/surgeons.html; do
  curl -s -o /dev/null -w "%{http_code} /$p\n" "https://orthoflowrecovery.com/$p"  # expect 200 each
done
gh api repos/SebbyServices/OrthoFlowRecovery/pages/builds/latest --jq '{status,commit}'  # expect built, HEAD
```

| Area | State |
|---|---|
| Agreement | Signed 2026-09-04. Paid. Commercial terms in `PRIVATE_NOTES.local.md` only |
| Live pages | `index.html`, `about.html`, `surgeons.html` and the same three in `es/`. Edit EN and ES together |
| `preview/` | Stale pre-launch copy, still tracked and served at `/preview/` (`noindex`). Not maintained: do not edit it or treat it as the site |
| `draft-preview/` | Gitignored, local-only draft layouts. Not the site |
| Copy | Approved by John: docx 2026-09-14, redlines 2026-09-16/18/22. Approval date sits in an HTML comment above each block |
| Patient reviews | Three on the homepage from the 2026-09-18 survey. Name use is limited to what each patient consented to (see the HTML comment) |
| Legal pages | `privacy.html`, `terms.html` live with "DRAFT, NOT YET IN EFFECT" banners, placeholders, counsel notes, and a leftover `noindex`. Finalizing them is John's counsel's call |
| SMS pages | `sms-terms.html`, `sms-privacy.html` live 2026-09-30 in John's wording, linked from every footer. Keep both live |
| Fonts / colors | Playfair Display + Inter, navy tokens. Client's proposed Poppins + Source Sans 3 NOT confirmed in writing. Do not swap fonts or color tokens in `styles.css`; layout rules are fine to change |
| Asset versions | `styles.css?v=20260930d`, `main.js?v=20260930` on all 11 pages. Bump on every CSS/JS change |
| Enquiry forms | Wired in EN and ES: `mjyvjwlq` reserve, `xaeyaokw` practice. Reserve form gained name split, ZIP, contact preference, and required SMS consent 2026-09-30 (John's approval verbal only). End-to-end delivery to John not confirmed on record |
| Surgeons compliance note | Commented out in `surgeons.html` pending healthcare attorney review |
| Business hours | Mon-Fri 8am-6pm, Sat 9am-4pm, Sun by appointment (filled 2026-09-14) |
| DNS / Pages | Fully live. A/AAAA resolve, HTTPS cert covers apex and `www`. Build type `legacy`. An old GoDaddy builder site still answers for the domain: see DNS and Deploy |

**Open decisions (ask Sebby, do not guess):** font/color confirmation, sibling client positioning, final legal page wording (counsel), written confirmation of the 2026-09-30 reserve-form fields, John's review of the Spanish SMS consent wording.

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

# 1. Shared-chrome drift across the six marketing pages (EN at root, ES in es/).
#    Expect exactly FIVE diffs per subpage, all intended: #reserve in nav, mobile
#    menu, and footer, plus the language-switcher link in nav and mobile menu.
#    One-line HTML comments are filtered (es/index.html's footer has extras).
chrome() { sed -n "$1" "$2" | command grep -v '^[[:space:]]*<!--.*-->[[:space:]]*$'; }
for dir in . es; do
  for page in about surgeons; do
    for range in '/<nav>/,/<\/nav>/p' '/<footer>/,/<\/footer>/p' '/<div class="mobile-menu">/,/<main/p'; do
      diff <(chrome "$range" $dir/index.html) <(chrome "$range" $dir/$page.html)
    done
  done
done

# 2. Em dash sweep. Must print nothing. Use `command grep` (plain grep is a ugrep
#    wrapper respecting .gitignore, which silently skips PRIVATE_NOTES.local.md).
LC_ALL=C command grep -rn $'\xe2\x80\x94' --include='*.html' --include='*.css' --include='*.js' --include='*.md' .

# 3. Placeholder sweep. Live marketing pages and styles.css must all be zero.
#    privacy.html and terms.html show 1 each until counsel finalizes them.
command grep -c '\[.*placeholder\|TODO\|REPLACE_WITH\|\[Insert' index.html about.html surgeons.html es/*.html styles.css privacy.html terms.html
```

```bash
# Verify #reserve links (sweep 1 misses the bottom CTA band, which sits in <main>)
command grep -c 'href="index.html#reserve"' about.html surgeons.html es/about.html es/surgeons.html  # expect 4 each
command grep -c 'href="#reserve"' index.html es/index.html                                            # expect 4 each
```

---

## Architecture

Three flat marketing pages at the repo root (`index.html`, `about.html`, `surgeons.html`) with Spanish copies in `es/` that reach shared files via `../`. Supporting pages at the root, English only: `privacy.html`, `terms.html`, `sms-terms.html`, `sms-privacy.html`, `404.html`. One `styles.css`, one `main.js`. No templating, no build step.

**Site layout:** The site went live 2026-09-22 when `preview/` was promoted to the root and the holding page retired (`ae071d1`). `preview/` is still tracked and served at `/preview/` with `noindex`, but it is frozen pre-launch markup: never edit it as if it were the site. Each marketing page's language switcher links to its sibling, so add, rename, or remove marketing pages in EN/ES pairs. ES pages link supporting pages as `../privacy.html` and so on; a bare `privacy.html` from `es/` 404s.

**Page 3 (`surgeons.html`):** Audience is surgeons, practice managers, coordinators, ASC/discharge staff. Compliance-note section is commented out in EN and ES until a healthcare attorney approves wording. No referral-incentive language anywhere on this page.

**Enquiry forms (Section 5.3 of signed agreement):**
- Reserve form fields: name, phone, email, timing-range `<select>` only ("within 2 weeks", "2 to 6 weeks", "6 or more weeks", "not sure yet"). Plus one SMS consent checkbox (`sms_consent`), added 2026-09-30 at John's written request for Spruce Health carrier registration. Unchecked by default; made required to submit the same day (Sebby's decision), and John's closing sentence "Consent is not a condition of purchase." was removed from the EN and ES labels to match. The matching sentence in `sms-terms.html` was removed too. It links to `sms-terms.html` and `sms-privacy.html`; keep both pages live and the wording verbatim.
- 2026-09-30, at Sebby's request (modeled on NICE's intake form): name split into `first_name`/`last_name`, plus required `zip` (5 digits, no State field because the service area is all Florida) and required `contact_preference` radios (phone/text/email). None of these are PHI. They go beyond the 5.3 list; John approved them verbally on a call with Sebby on 2026-09-30 (written confirmation not yet on file). `contact_preference` and `sms_consent` are both plain HTML `required`; no JS.
- NICE's form also asks for physician name, body part, surgery date, coverage program (student athlete, workers' comp, VA/DoD/military), and free-text comments. These stay off this site: 5.3 bans them and Formspree has no BAA. See the coverage-interest plan in memory before reopening this.
- Practice form fields: name, phone, email only.
- Never add: free-text medical field, surgery date, symptom/diagnosis, insurance, or any field that reveals a health event about a named person.
- Both show `.form-notice`: "Please do not include medical information in this form. We will contact you to discuss any specifics by phone."
- Formspree: `mjyvjwlq` reserve, `xaeyaokw` practice (John's own account). First submission may require John to confirm a Formspree activation email.

**Nav, mobile menu, footer** are copy-pasted into all 11 pages (six marketing, five supporting). A chrome change means 11 edits, with the ES strings translated. `privacy.html`, `terms.html`, and `404.html` still carry pre-launch chrome (`ortho-flow-wordmark.png`, `ortho-flow-logo-reverse.png`). Intended divergence on the marketing pages: subpages use `index.html#reserve` in four places (nav CTA, mobile-menu CTA, bottom CTA band, footer link) where the homepage uses `#reserve`, and each language switcher points at its own sibling. Sweep 1 catches all but the CTA band; the `#reserve` grep catches all four.

`.mobile-menu` is outside `<nav>` on purpose. A positioned ancestor traps the fixed overlay.

**`main.js` gotchas:**
1. Fade-in CSS is injected at runtime (`main.js` appends a `<style>` with `.fade-out`/`.fade-in`/`@keyframes fadeInUp`). Not in `styles.css`. A section that never intersects stays invisible.
2. Form handler binds `document.querySelector('form')` (first form only). Safe because each page has exactly one form. Would break if a second form landed on the same page.
3. `setActiveNavLink()` only touches `.nav-links a`. Mobile menu links never get `.active`.
4. Form status and button text come from `formText`, keyed on `<html lang>`. Change the English and Spanish strings together.

**Asset versioning:** every page links `styles.css?v=YYYYMMDD` and `main.js?v=YYYYMMDD` (11 pages, `../` on `es/`). When either file changes, bump the token on all of them in the same commit. Otherwise returning visitors get the new HTML with the old CSS/JS for up to 10 minutes (GitHub Pages sends `max-age=600`). That is what broke the SMS checkbox styling on 2026-09-30.

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

**Leftover GoDaddy Website Builder site (found 2026-09-30, not yet fixed).** A GoDaddy builder site for this domain was published 2026-05-05 (`orthoflowrecovery.godaddysites.com`). GoDaddy's builder servers (`13.248.243.5`, `76.223.105.230`) still answer for `orthoflowrecovery.com` with a valid GoDaddy cert (expires 2026-11-19). Any visitor whose DNS lookup reaches those IPs sees the old GoDaddy site with no browser warning; its `/about.html` is a GoDaddy "Page Not Found" (John hit exactly this on 2026-09-30). Browsers that visited before the 2026-09-05 cutover may also still hold its service worker (`/sw.js`), which serves a cached GoDaddy homepage at `/`. Fix: disconnect the domain from that builder site in John's GoDaddy account, then immediately re-run the DNS checks above plus `dig +short orthoflowrecovery.com A` (expect only the four GitHub IPs). GoDaddy can rewrite the apex A records when a builder site is disconnected or republished.

```bash
# 200 here means GoDaddy is still serving the domain; expect a connection failure or non-200 once fixed
curl -sk --resolve orthoflowrecovery.com:443:13.248.243.5 -o /dev/null -w '%{http_code}\n' https://orthoflowrecovery.com/
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

## Open Items

Launch items closed by 2026-09-22 (promotion, copy sign-off, pricing, hours, hero image, social icons, `noindex` removal) are in git history.

- [ ] **Disconnect the domain from the GoDaddy builder site** (see DNS and Deploy). Needs John's GoDaddy login
- [ ] Font and color confirmation from client in writing
- [ ] Healthcare attorney review of the surgeons-page compliance line (EN and ES)
- [ ] Counsel finalizes `privacy.html` and `terms.html`; then remove their DRAFT banners, placeholders, counsel notes, and `noindex`
- [ ] End-to-end test both Formspree forms in EN and ES (John may need to confirm first submission)
- [ ] Written confirmation from John of the 2026-09-30 reserve-form fields
- [ ] John reviews the Spanish SMS consent wording
- [ ] Bring `privacy.html`, `terms.html`, `404.html` chrome up to date (current logos, nav actions)
- [ ] Resolve the remaining `[FACT NEEDED]` tags in `CONTENT_DECK.md` (11 as of 2026-09-30)
- [ ] Confirm NICE logo use and photography requirements (claims rules documented in `CONTENT_DECK.md` 2026-09-12)
- [ ] Official reversed logo from client's designer

---

## This Repo Is Public

Every tracked file is readable on GitHub. `_config.yml` keeps internal docs off the live site but not off GitHub. If the build type ever changes from `legacy` to GitHub Actions, `_config.yml` stops being honored: re-run `curl -o /dev/null -w '%{http_code}\n' https://sebbyservices.github.io/OrthoFlowRecovery/CLAUDE.md` (expect 404) after any Pages change.

Never save a contract, invoice, or proposal into this folder. `.gitignore` excludes `*.pdf` and `*.docx`. All private content goes in `PRIVATE_NOTES.local.md` only.

---

## Logo Assets

| File | Use |
|---|---|
| `assets/ortho-flow-wordmark-light.png` | nav, mobile menu |
| `assets/ortho-flow-logo.png` | og:image |
| `assets/ortho-flow-logo-reverse-v3.png` | footer (tagline removed per John's redline, `0e7929a`) |
| `assets/ortho-flow-wordmark.png`, `assets/ortho-flow-logo-reverse.png` | pre-launch versions, still on `privacy.html`, `terms.html`, `404.html` only |
| `assets/ortho-flow-icon.png`, `favicon.png` | favicon, square uses |
| `assets/ortho-flow-logo-master.png` | source of truth (excluded from live site) |

All logo files are client-owned per the signed agreement. Master is 960x640 raster: fine for web, not print. The reversed logo was recolored here; ask the client's designer for an official version.
