# CHANGELOG

Session history for the Ortho Flow Recovery site build.

---

- **Aug 25, 2026:** Skeleton scaffolded from the Elite Care architecture. Design system and JS ported, all client copy replaced with placeholders, brand tokens genericized, Formspree and contact details deliberately left unwired. Committed as `cfcdb98`. Added "START HERE" bootstrap section. Pushed to the public remote.

- **Aug 26, 2026:** Client sent the logo and contact details. Brand tokens replaced with the real navy, logo assets derived and wired across all three pages, favicon swapped to PNG, `noindex` added while the live site still shows placeholder copy. Device line confirmed as NICE. Logged the phone number collision and the patient testimonial compliance block as the two things gating contact details and social proof. Enabled Pages, no custom domain. `/init` audit pass: added the Commands sweeps, fixed subpage heading structure, removed dead anchors, added `_config.yml` to keep internal docs off the published site, drafted copy into `CONTENT_DECK.md` for client review.

- **Aug 29, 2026:** `/init` audit pass correcting drift between the tracked file and the actual repo state (stale commit references, contradictory Pages status, phantom SVG warning, undercounted `#reserve` asymmetry, completed work still listed as pending).

- **Sep 5, 2026:** Signed agreement arrived (client countersigned 2026-09-04), deposit paid, engagement active. Structural rebuild to match the agreement:
  - `culture.html` renamed to `surgeons.html` via `git mv`, rebuilt to spec (what OrthoFlow handles, what the office doesn't manage, three-step referral, coverage/response, compliance-note placeholder, practice form).
  - Vision, mission, and values moved into `about.html`.
  - Nav, mobile menu, and footer updated across all three files.
  - Reserve form's date field and free-text notes field removed (violated Section 5.3 field list). Replaced date with timing-range picklist. Added `.form-notice` to `styles.css` and the medical-information notice to both forms.
  - Phone ownership and business-listing gates cleared. Holding page built at the repo root (logo, phone, service area, "Now Taking Reservations"). Full three-page build moved to `preview/` since GitHub Pages can only serve one root `index.html`.
  - DNS wiring completed: all A/AAAA records resolve to GitHub Pages, HTTPS cert covers both apex and `www`, holding page and `/preview/` return 200 live. MX/TXT/`_dmarc` reverified unchanged.
  - Patient Brokering Act compliance line moved from `PRIVATE_NOTES.local.md` to `CONTENT_DECK.md` (it's future public copy pending attorney review, not a confidential detail).
  - A signed PDF was found sitting untracked in the repo root. Moved out. `.gitignore` hardened with `*.pdf` and `*.docx`.
  - Committed and pushed: `29a482c`, `977a07f`.

- **Sep 5, 2026 (second pass):** Verification sweeps: shared-chrome drift is exactly the three intended `#reserve` diffs, em dash sweep clean repo-wide, `#reserve` counts 4/4 everywhere. Hours confirmed Mon-Fri 8am-6pm from the agreement's cover page; Sat/Sun still open. Drafted "For Surgeons and Practices" page copy into `CONTENT_DECK.md` (marked UNAPPROVED, `[FACT NEEDED]` tags in place). Corrected stale "procedure date" references in the homepage draft. Design-direction doc's reserve-form mockup includes a "surgeon or practice" field that is superseded by the signed agreement's tighter Section 5.3 field list; don't add it.

- **Sep 9, 2026:** Both Formspree forms wired with real IDs in John's own account: `mjyvjwlq` (reserve, patient rental on `preview/index.html`) and `xaeyaokw` (practice, physician request on `preview/surgeons.html`). Not yet tested with a real submission.

- **Sep 12, 2026:** Confirmed OrthoFlow does not carry the ROCC. NICE1 assets wired into homepage. Homepage pricing section added with John's confirmed facts and content applied.
