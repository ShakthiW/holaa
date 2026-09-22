# holaa — Brand Voice Guide

**Status:** Reference document. Every example in this guide is either lifted verbatim from the
live marketing site source (`chatbot-demo-admin/src/components/landing/**`,
`src/lib/data/landing-data.ts`) or written to match its patterns precisely — this is a
description of a voice that already exists in shipped copy, not a new invention.

---

## 1. Voice in One Line

**We sound like the hotel's best concierge, not a SaaS vendor.** Warm, precise, and a little
literary — never stiff, never hypey, never robotic. We describe what a guest will *feel*, then
back it with a fact.

---

## 2. Two Registers — Know Which One You're In

holaa's copy operates in two distinct registers. Confusing them is the most common way brand
voice breaks down, so name which one you're writing before you start.

### Register A — Guest-Facing (in-product concierge voice)
This is the AI concierge talking directly to a hotel guest. First person plural / warm-staff
voice. Sensory, specific, present-tense. Example (from `landing-data.ts`, a live "concierge
response" sample):

> "At 6:15 AM, soft golden rays illuminate the private infinity plunge pool. Frame-by-frame,
> the ocean shifts from deep indigo to warm amber, with fresh sea breezes rolling over the
> cliffside."

### Register B — Brand/Marketing-Facing (holaa talking to hotel buyers)
This is holaa the company talking to a GM, owner, or revenue manager. Confident, direct,
business-literate — it earns trust by being precise about the business outcome (direct
bookings, OTA commission avoided), not by being flowery. Example (live hero copy):

> "Give every guest an AI concierge that knows your hotel, remembers who they are, and turns
> conversations into direct bookings — before they even arrive."

**Rule of thumb:** Register A can be lush and sensory because it's selling an *experience* to
a guest in the moment. Register B stays grounded and outcome-first because it's selling a
*business decision* to an operator who will be skeptical of hype. Never let Register A's
sensory density bleed into a pricing page, and never let Register B's business tone bleed into
in-widget guest copy.

---

## 3. Tone Attributes (in priority order)

1. **Warm, not saccharine.** Genuine hospitality warmth — like a concierge who's actually glad
   to help — not customer-service cheerfulness. Avoid exclamation points as a substitute for
   warmth.
2. **Precise over hypey.** We earn claims with specifics (numbers, named features, named
   integrations) rather than superlatives. "Skip the 15–25% OTA commission" beats "save money."
3. **Confident, not aggressive.** State the differentiator plainly and move on — we don't need
   to attack competitors by name to make the point land (see `hola_brand_context.md` §8 on how
   we position against chatbots and OTAs without naming them as enemies).
4. **A little literary, always in service of specificity.** Sensory language is allowed and
   encouraged in guest-facing and demo copy — but every sensory detail should be something a
   guest could actually verify on arrival, never generic "luxury" filler.
5. **Never robotic.** This is the platform's own explicit design principle (`project_brief.md`:
   *"The AI should never feel robotic. It should feel like the hotel's best concierge."*) — it
   applies to our own marketing copy about the product just as much as it applies to the
   product itself.

---

## 4. Vocabulary — Say This, Not That

| Say | Not | Why |
|---|---|---|
| AI concierge | chatbot / bot | "Chatbot" is explicitly named as the thing we're not, in our own Problem Statement copy ("robotic chatbot popups... turn a warm welcome into an IVR menu"). |
| direct booking(s) | sale(s) / conversion(s) | The business outcome is booking-specific and ties to the OTA-commission narrative; "conversion" is generic SaaS-speak. |
| guest | user / customer | We're describing hospitality, not a software product's userbase. |
| property / hotel / resort | client / account | Match hospitality-industry language, not SaaS-account language, when describing the buyer's business. |
| storytelling / sensory response | AI-generated content | We never describe our own output the way a generic AI-content tool would. |
| grounded / verified knowledge | trained on your data | "Grounded" and "verified" carry the trust claim; "trained on your data" sounds like a generic ML pitch and undersells the RAG architecture's actual guarantee (no hallucination). |
| concierge / your best staff member | assistant / agent (in external copy) | "Agent" is fine in internal/technical docs (it's the literal architecture term) but reads as generic SaaS jargon externally — "concierge" is the brand noun. |
| holaa (always lowercase) | Holaa / HOLAA | Brand mark is lowercase even at a sentence start — see `hola_brand_style_guide.md` §2. |
| WhatsApp concierge / guest WhatsApp messaging | "WhatsApp Business API" (in technical/precise copy) | The integration is real and two-way, but built on a self-hosted gateway, not Meta's official Cloud API — see `hola_product_offerings.md` §2.6. Fine to say "WhatsApp" and "concierge" freely; just don't name the official API in a technical or compliance context. |
| scan-to-chat / in-room concierge | "QR code chatbot" / "digital menu" | This is a full concierge conversation, not a static digital-menu QR — say so; "digital menu" undersells it badly. |
| no app required / no app download | "app-free" / "appless" | Match the exact phrasing already used in shipped product copy (the printable QR card itself) rather than inventing a new variant. |
| partner experience / commission tracking | "affiliate program" / "marketplace" (until the self-serve version ships) | "Marketplace" implies operators list themselves, which isn't built yet — see `hola_brand_context.md` §7. "Partner experience catalog with real commission tracking" is accurate and still a strong claim. |
| revenue influenced / booking influenced | "engagement" / "conversions" | These are the platform's own real analytics field names (experience and outbound-click analytics both use "influenced," not "conversion") — match the product's own precise language. |
| AI-drafted review | "review generator" / "fake reviews" | It drafts a review *from the guest's own structured answers*, and the guest chooses to post it — say so plainly; never imply the review is written without the guest's real input. |

---

## 5. Sentence Patterns That Sound On-Brand

Pull these directly from the live copy as templates:

- **The reframe headline** — take an expected phrase and twist it toward the emotional truth:
  *"Hotel websites are still stuck answering questions nobody asks."* /
  *"Guests don't book rooms. They book experiences."*
- **The sensory present-tense answer** — always what the guest *hears, sees, smells, feels*,
  time-stamped when possible: *"Around sunrise you'll usually hear the waves before you see
  them."*
- **The plain business-outcome line, no metaphor** — used for anything money- or ops-related:
  *"Built to pay for itself in direct bookings."* /
  *"Skip the 15–25% OTA commission."*
- **The short, declarative product-philosophy line** — used sparingly, as a section-ending
  thesis statement, always attributed: *"— the holaa design thesis"*.
- **The specific-not-vague CTA** — never "Learn more": *"Book a demo"*, *"Watch product tour"*,
  *"Talk to sales"*, *"Request integration spec"*.
- **The scan-to-chat call-to-action** — short, imperative, frictionless, straight from the
  shipped in-room QR card copy: *"Scan to chat with your concierge — in-room dining, spa
  booking & guest services 24/7 — no app download required."* Use this exact rhythm (imperative
  verb → what it's for → the friction it removes) for any QR/WhatsApp-entry-point copy.

---

## 6. Mechanics & Conventions

- **"holaa" is always lowercase**, in headlines, at the start of sentences, everywhere except
  literal legal/copyright lines where a proper-noun style guide might otherwise force a
  capital — when in doubt, keep it lowercase; it's a deliberate brand choice (see the wordmark
  itself, which is never capitalized).
- **Sentence-case headlines**, not Title Case: *"Everything your concierge needs, out of the
  box."* not *"Everything Your Concierge Needs, Out Of The Box."*
- **Em dashes for a mid-sentence turn or aside**, used often and deliberately — it's a
  signature rhythm of this voice (see nearly every example quoted above).
- **Numbers stay as numerals in stat callouts** ("15–25%", "+42.8%") for scannability, but
  spelled out in flowing sensory prose ("six-course tasting menu") — match whichever register
  you're in.
- **Avoid exclamation points.** Warmth comes from specificity and rhythm, not punctuation.
- **Quotation-marked "voice of the guest" lines** (testimonials, sample questions) use curly
  quotes and are always attributed by name + location/role — never anonymous.

---

## 7. Do / Don't Examples

| Do | Don't |
|---|---|
| "Give every guest an AI concierge that knows your hotel, remembers who they are, and turns conversations into direct bookings." | "Our AI-powered chatbot solution helps hotels increase conversions through automated guest engagement." |
| "This week is more expensive because it's peak whale-watching season." | "Dynamic pricing algorithm has adjusted rates based on demand signals." |
| "holaa reduced our front-desk phone volume by 65% while elevating guest satisfaction to a record 99.4%." (flagged `[ILLUSTRATIVE]` — see `hola_brand_context.md` §7 before using real customer stats this way) | "Leverage best-in-class AI to optimize your guest engagement funnel." |
| "Connects to the stack you already use." | "Seamlessly integrates with your existing technology ecosystem." |
| "5-minute setup · Compatible with Oracle Opera, Cloudbeds, Mews · SOC2 & GDPR compliant" (fact-dense trust footer) | "Enterprise-grade security you can trust!" |

---

## 8. Audience-Specific Notes

- **To hotel GMs/owners (primary B2B buyer):** lead with the business outcome (OTA commission,
  direct bookings, guest satisfaction), use Register B, back every claim with a specific
  mechanism (the 4-tier destination resolver, the grounded knowledge engine) rather than an
  adjective.
- **To guests (in-product, widget/WhatsApp copy):** full Register A — sensory, present-tense,
  warm, never mentions "AI," "platform," or "holaa" as a company unless the guest asks how the
  concierge works.
- **To technical/developer audiences (integration docs, API references):** precision beats
  warmth — this is the one context where dropping most of the sensory language is correct.
  Still avoid generic SaaS jargon (say "the RAG knowledge engine," not "our proprietary AI
  technology").

---

## 9. Related Documents

- **[[hola_brand_context]]** — the positioning and facts this voice is in service of
- **[[hola_brand_style_guide]]** — the visual system this voice appears inside
- **[[hola_product_offerings]]** — feature detail to draw specifics from (never write vague
  copy when a real, specific feature exists to cite instead)
