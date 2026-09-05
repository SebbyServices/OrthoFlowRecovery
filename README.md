# Ortho Flow Recovery

Marketing site for Ortho Flow Recovery, post-operative recovery equipment serving
Miami-Dade and Broward counties, with a second page addressed to referring surgeons and
practices.

**Status: signed and paid engagement, holding page live at the repo root, full build
in `preview/`.** The repo root is a simple holding page (logo, phone, service area,
"Now Taking Reservations") while DNS gets wired to this repo. The real three-page site
lives under `preview/`: structure is built, page 3 was rebuilt to the signed agreement's
spec, and both enquiry forms match its field restrictions, but it carries no approved
copy yet. See `CLAUDE.md`'s "START HERE" for the current state in full.

---

## Local Development

No build step. Serve the folder and refresh.

```bash
python3 -m http.server 8000
# holding page at http://localhost:8000/
# full build at   http://localhost:8000/preview/
```

## Structure

```
index.html           Holding page: logo, phone, service area, "Now Taking Reservations"
preview/index.html   Home: hero, benefits, equipment, process, pricing, story, reserve form
preview/about.html   About: story, stats band, why us, vision, mission, values, CTA band
preview/surgeons.html  For Surgeons & Practices: what we handle, referral steps, practice form
styles.css           All shared styles, plus a small inline block on the root holding page
main.js              All behavior for the preview/ pages
favicon.png          Real, client supplied
assets/              Real logo assets, derived from the client's lockup
CLAUDE.md             Operating manual, read this first
CONTENT_DECK.md       Client copy, business basics confirmed, page prose still unapproved
```

## Deploy

GitHub Pages **is enabled and building**, serving `github.io`. DNS wiring to
`orthoflowrecovery.com` is in progress, see the DNS section of `CLAUDE.md` for the exact
records, which of them are safe to touch, and which are this domain's live Microsoft 365
business email that must not be touched. It also documents the apex AAAA requirement
that cost four days on the Elite Care launch.

## Before This Launches

See "Open Items Before This Can Launch" in `CLAUDE.md`. The blocking ones are approved
copy, written font and color confirmation, an attorney's review of the surgeons page's
compliance line, and real Formspree form IDs for both enquiry forms.

## Do Not

- Reuse anything from the Elite Care Recovery repo beyond architecture. See "Hard
  Separation" in `CLAUDE.md`.
- Write placeholder marketing copy to make the site look finished. Placeholders are
  intentional and visible so nothing unapproved reaches the client.
- Save a contract, invoice, or proposal into this folder, even briefly. See "This repo
  is public" in `CLAUDE.md`.
