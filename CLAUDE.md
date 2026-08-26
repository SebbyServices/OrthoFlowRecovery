# CLAUDE.md

Guidance for Claude Code when working in this repository.

> Read this file first, every session, before touching code.

---

## Project Snapshot

- **Client:** Ortho Flow Recovery (Miami, FL)
- **Business:** Post-operative recovery equipment, serving Miami and surrounding areas
- **Owner contact:** John Pierce
- **Domain:** `orthoflowrecovery.com` (NOT yet wired to this repo, see DNS section)
- **Repo:** `github.com/SebbyServices/OrthoFlowRecovery`, **public**
- **Developer:** Sebby IT Consulting, Corp.
- **Status:** Skeleton only. No approved copy, no brand assets, no live form.

**Relationship to Elite Care Recovery:** John Pierce is the brother of Chris Pierce.
Elite Care Recovery is a **separate client** in a **separate repo**, serving the same
Miami market with post-op recovery equipment. Treat them as distinct businesses that
may compete. See "Hard Separation" below. This is not optional.

---

## Hard Separation from Elite Care Recovery

This skeleton borrowed Elite Care's **architecture and design system only**. Everything
below is forbidden to carry across:

- **Never copy Elite Care's prose.** Their homepage story is about the two Pierce
  brothers together. It cannot describe one brother's separate company.
- **Never reuse the Elite Care Formspree ID (`xeedwqvp`).** It routes leads into Elite
  Care's inbox. Ortho Flow needs its own form. The placeholder in `index.html` is
  `REPLACE_WITH_ORTHO_FLOW_FORM_ID`.
- **Never reuse the Elite Care phone number** `(786) 214-2659` or any
  `@elitecarerecovery.net` address.
- **Never copy Elite Care or NICE product assets.** The NICE1 is Elite Care's product
  line. Do not assume Ortho Flow distributes it. Confirm the device line first.
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

## Architecture

Three flat HTML pages sharing one stylesheet and one script.

### The nav, mobile menu, and footer are copy-pasted into all three pages

There is no templating. Any change to `<nav>`, `.mobile-menu`, or `<footer>` must be
applied **three times**. This was the #1 regression source on the Elite Care build.
Verify with:

```bash
diff <(sed -n '/<nav>/,/<\/nav>/p' index.html) <(sed -n '/<nav>/,/<\/nav>/p' about.html)
```

The only **intended** divergence: the reserve form lives on the homepage, so subpages
link `index.html#reserve` where the homepage links `#reserve`, in both the nav CTA and
the footer quick links. Preserve that asymmetry. Making them identical breaks the
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

### `main.js`: five behaviors, no framework, no DOMContentLoaded

Sticky nav at 50px, mobile menu, smooth scroll, Formspree submit, IntersectionObserver
fade-in, plus `setActiveNavLink()`.

Two things that surprise people:

1. **The fade-in CSS is injected at runtime.** `main.js` appends a `<style>` block
   defining `.fade-out` / `.fade-in` / `@keyframes fadeInUp`. Searching `styles.css`
   finds nothing. Every `section`, `.card`, and `.step-card` starts at `.fade-out`, so
   **a section that never intersects stays invisible**.
2. **The form handler binds `document.querySelector('form')`**, the first form on the
   page only. A second form gets no JS enhancement. It also `preventDefault()`s
   unconditionally.

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
dig +short elitecarerecovery.net A     # pattern reference
gh api repos/SebbyServices/OrthoFlowRecovery/pages --jq '.https_certificate.domains'
```

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

---

## Open Items Before This Can Launch

- [ ] Approved copy for all three pages (`CONTENT_DECK.md` is an empty template)
- [ ] Ortho Flow logo, then replace `assets/ortho-flow-logo.svg` and `favicon.svg`
- [ ] Brand colors, then replace the `--color-accent` placeholder in `styles.css`
- [ ] Confirm which recovery device line Ortho Flow distributes
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
- [ ] Subpages use `index.html#reserve`, homepage uses `#reserve`
- [ ] Sections alternate `.bg-cream` / `.bg-cream-alt` correctly
- [ ] Scroll every page fully, nothing stuck at `opacity: 0`
- [ ] Keyboard-only tab pass, focus states visible
- [ ] No console errors
- [ ] No remaining `[placeholder]` or `TODO` text before launch
- [ ] Lighthouse: Performance 90+, Accessibility 95+, Best Practices 95+

---

## Last Updated

- Aug 25, 2026: skeleton scaffolded from the Elite Care architecture. Design system and
  JS ported, all client copy replaced with placeholders, brand tokens genericized,
  Formspree and contact details deliberately left unwired.
