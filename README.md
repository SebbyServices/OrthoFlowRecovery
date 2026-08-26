# Ortho Flow Recovery

Marketing site for Ortho Flow Recovery, post-operative recovery equipment serving Miami
and surrounding areas.

**Status: skeleton.** Structure and design system are in place. No approved copy, no
brand assets, no live form. Not ready to show a client.

---

## Local Development

No build step. Serve the folder and refresh.

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Structure

```
index.html      Home: hero, benefits, equipment, process, story band, reserve form
about.html      About: story, stats band, why us, CTA band
culture.html    Vision, mission, values, objectives, CTA band
styles.css      All styles
main.js         All behavior
favicon.svg     Placeholder
assets/         Placeholder wordmark only
CLAUDE.md       Operating manual, read this first
CONTENT_DECK.md Approved client copy, currently an empty template
```

## Deploy

GitHub Pages is **not yet enabled**. There is deliberately no `CNAME` file.
Read the DNS section of `CLAUDE.md` before wiring the domain. It documents the apex
AAAA requirement that cost four days on the Elite Care launch.

## Before This Launches

See "Open Items Before This Can Launch" in `CLAUDE.md`. The blocking ones are approved
copy, the logo, the brand color, the device line, and a real Formspree form ID.

## Do Not

- Reuse anything from the Elite Care Recovery repo beyond architecture. See "Hard
  Separation" in `CLAUDE.md`.
- Write placeholder marketing copy to make the site look finished. Placeholders are
  intentional and visible so nothing unapproved reaches the client.
