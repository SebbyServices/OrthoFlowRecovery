# CONTENT_DECK.md

**Approved client copy for Ortho Flow Recovery. PARTIALLY FILLED as of 2026-09-05.**

This file is the single source of truth for every word on the site. Nothing goes into
the HTML unless it is here first, supplied or approved by the client.

Until this file is filled in, the site keeps visible `[placeholder]` text. Do not
substitute invented marketing copy. See "No copy invention" in `CLAUDE.md`.

**Updated 2026-09-05: several facts below moved from unconfirmed to confirmed, and the
page structure changed.** See `PRIVATE_NOTES.local.md` for the specifics, this file only
states what's safe to state publicly. The "Culture Page" section further down is now
stale, see the note at its head before using anything in it.

---

## Business Basics

- Legal name: **Ortho Flow Recovery LLC** (client supplied 2026-08-26)
- Owner: supplied. Held in `PRIVATE_NOTES.local.md`, not here.
- Phone: **confirmed and live**, on the root holding page. Still `[placeholder]` inside
  `preview/`, since that build isn't approved yet, but the number itself is no longer
  gated. See `PRIVATE_NOTES.local.md` for the number.
- Email: supplied. Held in `PRIVATE_NOTES.local.md`. Worth asking whether the client
  wants a role address such as `info@` on the public site rather than a personal one.
- Address: supplied, and it must **never** be published. See `PRIVATE_NOTES.local.md`.
  Wherever a street address might otherwise appear (footer, business listings), use the
  service area instead.
- Service area: **CONFIRMED.** See `PRIVATE_NOTES.local.md` for the exact wording. The
  markup still hardcodes the old, wrong text and needs updating once real copy goes in.
- Business hours: not supplied
- Device line distributed: **NICE** (confirmed 2026-08-26 by the client's own patient
  feedback document, which refers throughout to "the NICE machine"). The specific model
  is still unconfirmed. Do not write "NICE1" until John confirms it.
- Manufacturer attribution required: unconfirmed. Ask what NICE requires for logo use,
  product photography, and permitted claims.

> This file is tracked in a public repo. Contact details and anything from a document a
> client marked private belong in `PRIVATE_NOTES.local.md`, which is gitignored.

## Brand

- Logo file: supplied 2026-08-26 as `LOGO clean_large (Orthoflow).png`, 4096x2730 RGBA.
  Derived web assets committed under `assets/`. See "Logo assets" in `CLAUDE.md`. The
  current master is a 960x640 raster copy, sufficient for web but not print. A
  higher-resolution or vector source would let these be regenerated cleaner.
- Primary brand color: **#003677** navy, sampled from the logo. **A client-sent design
  direction proposes a slightly different resample and an expanded palette, not yet
  confirmed in writing.** See `PRIVATE_NOTES.local.md`. Do not change this value on that
  document alone.
- Secondary color: **#5DA0E2** sky blue. **Decorative only.** It measures 2.71:1 on the
  cream background and 2.90:1 under white, so it fails WCAG AA for text and buttons.
- Supporting gray: **#5C646F**, the color of RECOVERY in the logo. 6.02:1 on cream, safe.
- Fonts: currently Playfair Display + Inter. **A pending design direction proposes
  Poppins + Source Sans 3 instead, not yet confirmed.** See `PRIVATE_NOTES.local.md`.
- Tagline: **"Better Recovery. Delivered. Simplified."** (set in the logo lockup itself,
  so it is client authored, not invented). **Cannot go on the website as written.** "Better
  recovery" asserts an improved medical outcome, which the no-clinical-claims rule bars
  absent NICE-cleared wording supplied in writing. See "No clinical claims" in
  `CLAUDE.md` and `PRIVATE_NOTES.local.md` for where this stands.

## Homepage

- Hero headline:
- Hero subheadline:
- Benefits section title:
- Benefit 1 / 2 / 3:
- Equipment section title and description:
- Process steps 1 through 4:
- **Pricing section, all tiers shown together.** Figures not yet supplied. A per-day
  rate must never be shown alone, see `CLAUDE.md` Architecture.
- Story band headline and paragraph:
- Reserve section title and instruction line:

## About Page

Now also absorbs the vision, mission, and values material that used to sit on a
standalone Culture page, see below.

- Headline:
- Story paragraphs:
- Stats:
- Why-us reasons:
- Vision:
- Mission:
- Core values:
- CTA band headline and line:

## For Surgeons and Practices Page (replaces Culture)

New as of the signed agreement, 2026-09-04. Addressed to surgeons, practice managers,
surgical coordinators, and ASC or discharge staff, not patients. Not yet built in the
HTML, see `CLAUDE.md` Architecture for the rename that has to happen first.

- What OrthoFlow handles for the office:
- What the office does not have to manage:
- How to refer a patient, steps:
- Coverage and response times:
- **Required compliance line, PENDING ATTORNEY REVIEW, do not publish without sign-off:**
  > "There is no charge to your practice, and nothing is offered to your practice. The
  > patient pays us directly."

  This has to survive verbatim if used. It is a Florida Patient Brokering Act concern,
  not a copy preference: nothing of value may be offered to a referral source anywhere
  on this page, no fee, no rebate, no free equipment, no sponsored lunch, no practice
  discount. Do not draft additional referral language here from general marketing
  instinct without the same review.
- Practice enquiry form: name, phone, email only. No patient information, and the form
  must say so visibly. See `CLAUDE.md` Architecture for the full field-restriction rule.

## Compliance

- HIPAA or medical disclaimer language: not drafted. See `CLAUDE.md` Architecture for
  the field-level rules that are now a signed contractual term, independent of any
  disclaimer wording.
- Any claims requiring substantiation (delivery windows, response times): not drafted
- **Patient testimonials: BLOCKED.** Client supplied testimonial material exists but is
  not usable as website copy. Publishing any of it requires written per patient
  marketing authorization plus a legal read of the medical claims involved. Rationale
  and specifics are in `PRIVATE_NOTES.local.md`. The default answer is no.
- **Referral incentives: BLOCKED.** Nothing of value may be offered to a referral source
  anywhere on the surgeons and practices page. See that page's section above.

---

# DRAFT COPY FOR CLIENT REVIEW

**Status: UNAPPROVED. Nothing below is in the HTML, and nothing goes in until John signs
off line by line.** This exists so he can react to something concrete instead of a blank
form, which is faster than asking him to write from scratch.

Two rules shaped these drafts:

1. **Every benefit is about the service, not the machine.** The NICE1 is sold through a
   national dealer network, so identical hardware is available from other dealers
   including at least one in this market. The machine cannot differentiate this
   business. Delivery, setup, and follow-up can, and the client's own patient feedback
   shows that is exactly what patients thank him for.
2. **No clinical claims.** Nothing here says the device reduces pain, swelling, or
   medication use. Any such wording must come from what NICE is cleared to claim and
   should be lifted verbatim from the manufacturer, not written by us.

Anything tagged **[FACT NEEDED]** is a factual assertion about a real medical business.
Do not guess at these, do not soften them into vague copy, and do not publish the page
until John supplies them.

---

## Homepage

**Hero headline** (pick one)
- A. Recovery equipment, delivered and set up at home.
- B. Post-op recovery, without the logistics.
- C. Your recovery equipment, handled start to finish.

**Hero subheadline**
> Ortho Flow Recovery brings the NICE1 cold therapy and compression system to your door
> before surgery, sets it up, and stays with you until it goes back.
> **[FACT NEEDED: service area sentence]**

**Benefits section title:** Why patients choose Ortho Flow

- **Delivered and set up.** We bring the unit to you and set it up in the room where you
  will actually recover. Nothing to pick up, nothing to assemble.
- **A real person, the whole way through.** One point of contact from reservation to
  pickup. **[FACT NEEDED: confirm John is the single contact, or name the team]**
- **We come and get it.** When your surgeon clears you, we collect the equipment.
  No shipping, no return labels.

**Equipment section title:** The NICE1 cold therapy and compression system

> A single unit that combines cold therapy with programmable compression, with no ice to
> refill and no cooler to drain. **[FACT NEEDED: confirm specs, dimensions, and weight
> with NICE, and confirm what wording NICE permits dealers to use.]**

**Process, four steps**
1. **Reserve before surgery.** Tell us your procedure date and we hold a unit.
2. **We deliver and set up.** **[FACT NEEDED: delivery window. Do not write "24 hours"
   or "same day" unless John commits to it.]**
3. **We check in during recovery.** **[FACT NEEDED: cadence. His patient feedback shows
   he does this, so confirm what he wants to promise.]**
4. **We collect it.** Arranged around your follow-up appointment.

**Story band headline:** Built around the part nobody else handles
> **[FACT NEEDED: John's actual reason for starting this. One short paragraph in his own
> words. Do not invent an origin story.]**

**Reserve section title:** Reserve a unit for your procedure
**Instruction line:** Tell us your procedure date and we will confirm availability and
delivery. **[FACT NEEDED: response time commitment. The form currently promises a reply
within 24 hours in main.js. Either John commits to that or the wording changes.]**

---

## About Page

**Headline:** About Ortho Flow Recovery
**Story paragraphs:** **[FACT NEEDED]** Needs John's own account: what he did before,
why he started this, what he saw patients struggling with. This is the one section that
cannot be drafted for him without it becoming fiction.

**Stats band, "By the Numbers"**
> **[FACT NEEDED, and the highest risk section on the site.]** Publishing invented
> figures about a healthcare business is deceptive advertising. Every number must be one
> John can substantiate. Reasonable candidates to ask him for: units in service,
> patients served to date, number of referring practices, average delivery time.
> **If he does not have real figures, delete this band.** Do not round up, do not
> estimate, and do not use "hundreds of" as a hedge.

**Why-us reasons:** reuse the three service benefits from the homepage, expanded.

**CTA band headline:** Talk to us before your procedure

---

## Culture Page (superseded, see note)

**This standalone page no longer exists in the signed scope.** The vision, mission, and
values material below now belongs on the About page instead, see the outline above. It
is left here, unedited, only because the vision and mission drafts may still be useful
raw material for that section. Do not build a Culture page from this. Do not assume the
core values or objectives below are still wanted verbatim once they move to About.

These must reflect what John actually believes, not what reads well. Drafts are starting
points for a conversation with him.

**Vision:** Every patient recovers at home with the right equipment and someone
accountable for it.

**Mission:** To take the logistics of post-operative recovery equipment off the patient
and the surgical practice, by delivering, setting up, supporting, and collecting the
equipment ourselves.

**Core values, drafts**
- **Show up.** Delivery and pickup happen when we said they would.
- **Answer the phone.** A recovering patient should never reach a queue.
- **Explain it once, properly.** Setup is not finished until the patient can use it.
- **Stay in touch.** We check in during recovery, not just at delivery.

**Objectives:** **[FACT NEEDED]** Business objectives are John's to set.

**CTA band headline:** Recovering soon? Let's get you set up.

---

## Claims and compliance checklist, before any of this goes live

- [ ] Every **[FACT NEEDED]** above resolved by John in writing
- [ ] Device description wording cleared against NICE's approved dealer language
- [ ] No clinical outcome claims anywhere in the final copy
- [ ] Delivery, response, and pickup promises match what the business will actually do
- [ ] Stats band either populated with substantiated figures or removed entirely
- [ ] Medical disclaimer drafted, if John's counsel wants one
