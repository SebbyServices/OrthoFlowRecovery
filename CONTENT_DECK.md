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

**Same day, second pass:** weekday business hours confirmed off the signed agreement's
cover page (Sat/Sun still open, ask John). Two leftover "procedure date" references in
the homepage draft corrected to match the timing-range picklist actually built into the
form. Draft copy for the For Surgeons and Practices page added below, it had been an
outline only until now. None of this is approved. Every `[FACT NEEDED]` tag below still
blocks that section from going into the HTML.

**2026-09-08: John answered most of the open facts, in writing (docx via text).** Most
`[FACT NEEDED]` tags below are now resolved and marked so. Two answers are flagged
**BLOCKED, NOT USABLE AS WRITTEN** instead of being filled in, both are clinical-claim
problems under Section 10.3, the same category as the tagline issue, not filled in
until John and Sebby resolve them:
- His homepage headline pick, "Better Relief with Personal Support," asserts a medical
  outcome the same way "Better Recovery" did. Not going in as written.
- His answer under "Surgeons page headline" is a first-person founder/mission passage
  addressed to patients, not a headline, and says "KEEP CULTURE PAGE." It also contains
  a second claim, "pain and swelling more manageable." Reads like it was meant for the
  About page rather than the surgeons page, and raises whether he wants to revert the
  agreement's Section 1.1.3 page-3 swap, a scope question, not something to guess at.

Real numbers arrived for the pricing section for the first time, see the homepage draft
below. They are still John's raw figures, not approved final wording, the phrasing
below is a draft for him to react to like everything else in this file.

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
- Business hours: **Mon-Fri, 8:00 AM to 6:00 PM, confirmed on the signed agreement's
  cover page (2026-09-05).** John confirmed 2026-09-08 there are no weekend deliveries.
  That answers the delivery-scheduling question, not necessarily whether the phone line
  itself is closed Sat/Sun, worth a one-line confirmation before the footer's Sat/Sun
  rows say "Closed" outright.
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
  **RESOLVED 2026-09-08: John confirmed in writing, remove the tagline from the website
  for now.** Nothing to draft here, just drop it. He separately asked about removing the
  tagline from the logo itself, which is a different, unconfirmed question, see
  `PRIVATE_NOTES.local.md`.

## Homepage

- Hero headline:
- Hero subheadline:
- Benefits section title:
- Benefit 1 / 2 / 3:
- Equipment section title and description:
- Process steps 1 through 4:
- **Pricing section, all tiers shown together.** Figures supplied 2026-09-08, draft
  wording in the "DRAFT COPY FOR CLIENT REVIEW" section below. A per-day rate must never
  be shown alone, see `CLAUDE.md` Architecture.
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

**BLOCKED 2026-09-08: John's pick, "Better Relief with Personal Support," is not usable
as written.** "Better relief" asserts a medical outcome, the exact same problem as the
"Better Recovery" tagline. Cannot go in without NICE's exact cleared wording in writing,
per Section 10.3. His intent, relief plus personal, human support, is a fine direction
for a claim-free rewrite, options to send back to him:
- D. Comfort and support, delivered to your door.
- E. Personal support, every step of recovery.
- F. The comfort of home, with support you can count on.
Still showing option A below until he picks a claim-free version.

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
1. **Tell us your timeframe.** Reserve a unit with a general window, not a procedure
   date. **[Matches the reserve form's timing-range picklist: within 2 weeks, 2 to 6
   weeks, 6 or more weeks, or not sure yet. No date field, per the signed agreement's
   HIPAA-shaped form rules, see `CLAUDE.md` Architecture.]**
2. **We deliver and set up.** **RESOLVED 2026-09-08:** deliveries and pickups run
   Mondays and Thursdays. Draft wording: "Delivery is scheduled around your procedure
   date, typically the closest Monday or Thursday, with your rental period starting the
   day of surgery." No exact procedure date is ever collected by the form itself, this
   sentence describes the general pattern, not a specific appointment.
3. **We check in during recovery.** **RESOLVED 2026-09-08:** two check-ins during the
   rental, one the day after surgery, one a few days before the unit is due back. Draft
   wording: "We check in twice during your rental, the day after your procedure and
   again as it winds down."
4. **We collect it.** Arranged around your follow-up appointment.

**Pricing, all tiers together** (Section 1.1 puts this between process steps and reasons
to choose) **RESOLVED 2026-09-08**, real figures from John, draft wording only:
- Two-week rental: $25/day, 14-day minimum ($350 total).
- Longer than two weeks: as low as $150/week after that (never state the underlying
  $21.43/day figure by itself, the signed agreement bars a lone per-day number since it
  understates the real cost, always pair it with the 14-day tier like this).
- Delivery and pickup: included at no extra charge.
- Fit adjustments or equipment issues during the rental: serviced at no charge.
- Unit returned, then rental extended: $50 re-delivery fee.

Draft sentence: "Two weeks minimum at $25 a day, delivery and pickup included. Need it
longer? As low as $150 a week after that. Any fit or equipment issue is serviced free."

**Story band headline:** Built around the part nobody else handles
> **[FACT NEEDED: John's actual reason for starting this. One short paragraph in his own
> words. Do not invent an origin story.]**

**Reserve section title:** Reserve a unit
**Instruction line:** Tell us your general timeframe and we will confirm availability
and delivery. **RESOLVED 2026-09-08:** John commits to same-day response, next business
day at the latest, by call or text. Draft wording: "We respond the same day, next
business day at the latest." Still needs wiring into the success message in `main.js`
once approved, see that file's note about not promising a time nobody agreed to.

---

## About Page

**Headline:** About Ortho Flow Recovery
**Story paragraphs:** **RESOLVED 2026-09-08, John's own words, sent in writing:**

> OrthoFlow was founded after seeing how difficult the first days and weeks after
> orthopedic surgery can be, not only for patients, but also for the practices caring
> for them.
>
> Patients often leave surgery facing pain, swelling, limited mobility, and uncertainty
> about what comes next. Traditional ice can be inconvenient and inconsistent, while
> purchasing advanced recovery equipment may be impractical. Even when better technology
> is available, arranging the equipment, learning how to use it, and managing its return
> can become another burden during an already demanding time.
>
> We also saw the challenge from the practice's perspective. Surgeons and their staff
> want patients to feel supported after they leave the office, but they do not have the
> time or resources to coordinate equipment deliveries, answer every product question,
> or manage rental logistics.
>
> OrthoFlow was created to help close that gap.
>
> We provide advanced cold and compression equipment directly to the patient's home, set
> it up, explain how it works, and remain available throughout the rental. When the
> patient is finished, we coordinate the pickup as well. Our goal is to make the entire
> experience simple for the patient and require as little involvement as possible from
> the referring practice.

Checked against the no-clinical-claims rule: describes what patients generally face
after surgery and what OrthoFlow does logistically, does not claim the device itself
reduces pain, swelling, or recovery time. Reads clean, no changes needed for that rule,
still needs John's final sign-off as with everything else in this file.

**Stats band, "By the Numbers": RESOLVED 2026-09-08, drop it for now, John's own call.**
Remove the section from `preview/about.html` entirely rather than leave it empty. This
matches the fallback this file already recommended when no substantiated figures exist.

**Why-us reasons:** reuse the three service benefits from the homepage, expanded.

**CTA band headline:** Talk to us before your procedure

---

## For Surgeons and Practices Page

Written to the section headings already scaffolded in `preview/surgeons.html`. Same
rules as above, plus two specific to this page: no referral-incentive language anywhere
(see the compliance line further up), and the compliance line itself must survive
verbatim, not be paraphrased or expanded on here.

**Hero headline** (pick one)
- A. Built for referring practices, not just patients.
- B. A recovery equipment partner your office doesn't have to manage.
- C. One call away for your post-op patients.

**BLOCKED 2026-09-08: John's answer here was not a headline.** He wrote "KEEP CULTURE
PAGE" followed by two paragraphs in first person addressed to patients, about
"modern therapies that can make pain and swelling more manageable," his role, and
OrthoFlow's culture. Three separate problems, none resolved by guessing:
1. It reads like About-page mission material, not something addressed to surgeons and
   practice staff, this page's actual audience.
2. "KEEP CULTURE PAGE" may mean he wants the old standalone Culture page back instead of
   this page. That reverses a structural decision the signed agreement already made in
   Section 1.1.3. A scope question for Sebby and John to settle in writing, not something
   to build from a one-line aside.
3. "Pain and swelling more manageable" is a clinical claim, same Section 10.3 problem as
   the headline and tagline. Would need rewriting even if it does end up on the site.
Still showing option A below until this is sorted out. See `PRIVATE_NOTES.local.md`.

**Hero subheadline**
> Ortho Flow Recovery delivers, sets up, and collects post-operative recovery equipment
> directly with the patient, serving Miami-Dade and Broward, so your office never has to
> coordinate any of it.

**"What OrthoFlow Handles" section title:** What we handle for your patients
- Delivery and setup, Mondays and Thursdays, scheduled around the procedure date.
  **RESOLVED 2026-09-08, same figure as the homepage process steps.**
- Check-ins during recovery, twice per rental. **RESOLVED 2026-09-08, same cadence as
  homepage.**
- Pickup once the surgeon clears the patient. No return shipping, nothing for the office
  to track.

**"What Your Office Doesn't Have To Manage" section title:** What comes off your plate
- No equipment inventory to stock, store, or maintain.
- No delivery or pickup logistics for staff to coordinate.
- No billing conversations. Patients handle payment directly with us.

**"Referring A Patient" steps, three step-cards**
1. **Recommend Ortho Flow.** **RESOLVED 2026-09-08: in-person recommendation only, no
   card or handout exists.** Draft wording should not promise or depict a card.
2. **Patient reserves.** They contact us directly with their general timeframe, the same
   non-clinical picklist used on the homepage form.
3. **We handle the rest.** Delivery, setup, check-ins, and pickup, without involving
   practice staff.

**"Coverage & Response" cards**
- Coverage area: Miami-Dade and Broward counties.
- Response time to practices: **[FACT NEEDED. Distinct from the Website Care support
  response times in the signed agreement, which cover Designer's response to Client, not
  Client's response to a referring office.]**

**Compliance Note section:** uses the required compliance line already recorded above,
verbatim, pending attorney review. Do not draft additional copy in this section beyond a
short lead-in sentence that introduces the box, for example "A note on how this works
financially:" with no further elaboration.

**"For Your Office" section title:** Refer a patient
**Instruction line:** Send us your patient's name, phone, and email; we'll take it from
there. No patient information needed, and please don't include any.

**CTA band headline:** Have a patient who needs equipment?
**CTA supporting line:** **[FACT NEEDED: a short closing line, John's choice of tone.]**

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
