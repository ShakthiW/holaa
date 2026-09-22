# holaa — Brand Context

**Status:** Reference document. Maintained by Marketing. Re-verify any figure marked
`[PLACEHOLDER]` or `[ILLUSTRATIVE]` against Sales/Product before it leaves this workspace in
externally-published material.

**Sources this document is built from:** `docs/project_brief.md`, `docs/platform_features.md`,
`docs/multi_tenant_provisioning_and_theming.md`, `docs/holaa.pdf` (brand mark), the live
marketing site source (`chatbot-demo-admin/src/components/landing/**`,
`src/lib/data/landing-data.ts`), and `chatbot-demo-admin/src/app/globals.css` (design tokens).
Where the codebase and the docs disagreed, the docs won (they're dated more recently and are
maintained specifically for accuracy — see §7 "What's Real vs. What's Illustrative").

---

## 1. Company & Product Snapshot

| | |
|---|---|
| **Product name** | holaa (always lowercase, even at the start of a sentence — see the Voice Guide) |
| **Category** | AI Hospitality Experience Platform — not a "hotel chatbot" |
| **Engineering org** | Standord-AI (the parent org that builds and operates the platform; "holaa" is the market-facing brand) |
| **Model** | Multi-tenant B2B SaaS. Every hotel gets its own admin dashboard + guest-facing concierge, provisioned from a shared template and billed on a per-property subscription. |
| **Primary buyer** | Hotel/resort General Managers, Revenue Managers, and independent boutique-property owners |
| **Primary user (guest side)** | Hotel guests and prospective guests, pre-arrival through post-stay |
| **Geography of origin** | Built and first deployed for Sri Lankan luxury resorts and boutique hotels (the "Sri Lanka Experience Layer" is a named, shipped differentiator — see `hola_product_offerings.md`), expanding to international luxury/boutique hospitality generally |
| **Deployment** | Each hotel gets a dedicated Next.js admin app (`<slug>-admin`, deployed on Vercel) talking to a shared multi-tenant Go API + Postgres + Qdrant vector store |

---

## 2. Positioning Statement

> For luxury and boutique hotels losing direct bookings to OTAs and generic chat widgets,
> **holaa** is the AI concierge platform that talks to guests the way a hotel's best staff
> member would — with real knowledge of the property, sensory storytelling instead of spec
> sheets, and a straight line from "I'm curious" to a confirmed direct booking. Unlike
> generic hospitality chatbots, holaa is built around a **grounded knowledge engine** (it only
> speaks from a hotel's own verified content) and a **storytelling response layer** (it answers
> the emotional question, not just the factual one).

This is the sentence every other positioning line in this workspace should trace back to.
It is derived directly from `docs/project_brief.md`'s "Product Philosophy" section and the
platform's own tagline used site-wide: *"Every great stay starts with a holaa."*

---

## 3. Mission, Vision, Philosophy

- **Vision** (from `project_brief.md`): an intelligent guest engagement ecosystem that
  transforms how travellers discover, book, and experience hotels — functioning as an
  extension of the hotel's own hospitality team, not a bolt-on support widget.
- **Operating principle:** *"Every conversation should increase the likelihood that the guest
  books the hotel."* Every feature, every UI card, every line of copy should be evaluated
  against this — does it create excitement, reduce uncertainty, or build trust?
- **The one-line test for "does this feel on-brand":** *the AI should never feel robotic — it
  should feel like the hotel's best concierge.*

---

## 4. The Problem We Solve

Modern travellers make expensive booking decisions based on emotional questions that static
hotel websites are structurally bad at answering:

- "What does sunrise look like from the balcony?"
- "Is the beach crowded in the morning?"
- "Will my parents enjoy this hotel?"
- "Is December a good time to stay here?"

Hotels currently answer these with room-spec PDFs, image galleries, and generic FAQ chatbots —
none of which build the desire that actually converts a browsing visitor into a guaranteed
direct booking. Guests bounce to TripAdvisor, Instagram, or an OTA search instead, and the
hotel pays a 15–25% commission for a booking it could have taken directly.

**The core thesis** (used verbatim on the marketing site): *"Guests don't book rooms. They book
experiences."*

---

## 5. Who We Serve

Four segments, mapped directly to the four live pricing tiers (see `hola_product_offerings.md`
for full detail — pricing figures there are marked placeholder):

| Segment | Property profile | What they need most |
|---|---|---|
| **Starter** | A single independent property "finding its feet" | A credible AI concierge live on the website fast, without a big lift |
| **Discover** | Boutique hideaways & lodges | Itinerary planning, guest memory, in-room QR — a fuller guest journey |
| **Engage** | Luxury resorts & ocean villas (flagship segment — "Most popular" tier) | Multichannel distribution, curated experiences, full revenue analytics |
| **Inspire** | Enterprise hotel collections / multi-property groups | Live human handover, frontier-tier AI, unlimited knowledge base, white-glove onboarding |

**Buyer persona shorthand:** a GM or owner-operator who feels the OTA commission tax
personally, is proud of the property's atmosphere and story, and is skeptical of "just another
chatbot" — they need to see the storytelling and sensory-detail difference to believe it.

---

## 6. What We Offer (pointer)

Full feature inventory, prioritized and ranked, lives in **[[hola_product_offerings]]**. In
one paragraph: an AI concierge (multi-agent: Concierge, Booking, Dining & Spa, Itinerary) that
answers guests with grounded, storytelling responses pulled from the hotel's own uploaded
knowledge; renders rich generative-UI cards (room carousels, dining menus, itinerary timelines,
booking confirmations) inline in the conversation; routes guests to the hotel's preferred
direct-booking destination or OTA with full click-tracking; remembers returning guests; and
gives hotel staff a full operations dashboard (knowledge management, bot persona config,
analytics, live chat handover) to run it.

---

## 7. What's Real vs. What's Illustrative

This matters for anyone drafting external copy from this workspace — do not blur these lines:

| Category | Status | Detail |
|---|---|---|
| Feature set (multi-agent AI, RAG knowledge engine, generative UI cards, memory engine, omnichannel booking routing, dashboard) | **Real, shipped** | Verified directly against `docs/platform_features.md`, a codebase-derived audit. |
| Pricing figures ($190/$490/$990/Custom) | **`[PLACEHOLDER]`** | The codebase comment above `PRICING_PLANS` in `landing-data.ts` states these dollar figures exist nowhere else in the system — the backend only stores feature-gating flags, not prices. Do not quote these externally without Sales/Finance sign-off. |
| Hotel logos shown as "Trusted by" (Amanwella, Wild Coast, Ceylon Tea Trails, Galle Fort Hotel, Capella, One&Only) | **`[ILLUSTRATIVE]`** | These are real luxury hospitality brands used as aspirational placeholder logos on the demo marketing site — not confirmed holaa customers. Do not present as a client list. |
| Executive testimonials (Marcus De Silva/Amanwella, Eleanor Vance-Cross/Ceylon Tea Trails) and stats (+42.8% direct booking lift, 99.4% CSAT) | **`[ILLUSTRATIVE]`** | Demo-site placeholder copy in the brand voice, not verified customer results. Replace with real case studies as they exist. |
| WhatsApp integration | **Real, shipped, but not the "WhatsApp Business API"** | Implemented via a self-hosted OpenWA gateway (`whatsapp-web.js`/`baileys`), not Meta's official Cloud API, despite the integrations page listing "WhatsApp Business API" as the partner name. Say "WhatsApp concierge" or "guest WhatsApp messaging," not "official WhatsApp Business API," in precise/technical copy. |
| PMS integrations (Oracle Opera, Cloudbeds, Mews) | **Adapter architecture shipped; live 2-way sync is the stated V1 direction, not yet the shipped default** | V1 ships in **External Booking Engine Mode** — holaa routes guests to the hotel's existing booking engine/OTA rather than holding live 2-way PMS inventory sync. The PMS adapter interface exists and is designed for this; treat "instant 15-minute room holds" and "live inventory sync" as near-term roadmap, not the default V1 guest experience, unless a specific property has Integrated Mode enabled. |
| SOC2 Type II / GDPR / AES-256 compliance claims | **Unverified in this workspace** | Repeated on the marketing site and FAQ; no compliance audit artifact was found alongside the code during this research pass. Flag for legal/security confirmation before repeating in a sales or compliance context. |
| 45+ language support | **Unverified as a hard product ceiling** | Stated on the marketing site; the AI agent is LLM-based and multilingual by nature, but no explicit "45 languages" configuration or test matrix was found in the docs. Treat as a directional claim, not an exact spec, until confirmed. |
| Voice Concierge, Digital Twin, Computer Vision Search, AR Hotel Guide, Predictive Hospitality AI, Cross-Hotel Network Intelligence, Sustainability Assistant | **Roadmap / not yet shipped — zero code exists** | Listed under "Future Roadmap" in `project_brief.md`, and Voice Concierge + Digital Twin are even listed as if shipped in the landing page's own `CORE_FEATURES` array — but a direct code audit found no voice, 3D, or digital-twin implementation anywhere in the app. Never present these as current capabilities under any circumstance. |
| Experience Marketplace | **Partially shipped — reclassify, don't call it pure roadmap** | `project_brief.md`'s "Future Roadmap" describes a self-serve, two-sided marketplace where *verified local operators list themselves*. That self-serve/verification layer isn't built. But the underlying hotel-side capability — a staff-curated catalog of partner experiences with real commission-rate and guest-discount fields, surfaced by the AI itinerary generator and tracked with real revenue-attribution analytics — **is fully shipped**, as the "Guest Experience Engine" (`/dashboard/experience`). See `hola_product_offerings.md` §2.8. Say "partner experience catalog with commission tracking" for the real, shipped thing; reserve "Experience Marketplace" for the still-roadmap self-serve-operator vision specifically. |
| Single-item AI recommendation (`get_personal_recommendation` tool / `PersonalRecommendationUI`) | **Real tool and UI, but the recommendation logic is a hardcoded demo payload** | Always returns the same fixed "Beachfront Plunge Pool Villa" result regardless of the guest's actual stated preferences — not yet wired to real guest data or the Experience Engine catalog. Don't describe this specific tool as "AI-personalized upselling"; the Experience Engine (`hola_product_offerings.md` §2.8) and the itinerary generator are the real, working parts of the upsell story. |
| Channels beyond WhatsApp + web widget | **Partially aspirational** | Only **WhatsApp** and the **embeddable web widget** are live, working channels today, plus two narrower guest-facing surfaces: an **in-room QR ordering flow** (`/q/[propertyId]/[roomId]`) and a **post-stay survey** flow. The inbound message API is architected channel-generically (so Messenger/Instagram could plug in later) but explicitly rejects any channel other than `whatsapp` today. Facebook Messenger, Instagram DMs, kiosks, reception tablets, and voice assistants — all listed under "Omnichannel Deployment" in `platform_features.md` — are not live. |
| AI Feedback Console (dashboard) | **Placeholder UI, not real** | The dashboard's `/dashboard/glossary` page (an "AI Feedback Console" for approving/improving/retraining AI answers) runs on hardcoded mock data and is labeled in-app "Placeholder UI (Backend API Coming Next)." Its "Retrain" action only fires a toast notification. Do not describe a live continuous-learning feedback loop. |
| Bot persona `personality_traits` | **UI-only, not persisted** | Staff can select personality traits in Settings, but the value isn't saved server-side yet (explicit in-code TODO). Don't promise multi-select personality tuning as a working feature; `tone_preset`, `response_length`, and `greeting_style` are the settings that actually persist and take effect. |
| "Native 2-way PMS API connectors," "under 48 hours" PMS setup, "5–7 business day" onboarding | **Existing marketing claims, independently unverified** | Repeated in the landing-page FAQ; a PMS adapter *interface* exists in the backend, but this codebase doesn't contain connector implementations deep enough to independently confirm the specific timelines. Treat as claims to confirm with Product/Engineering, not newly-verified facts. |

---

## 8. Competitive Landscape (as referenced in our own docs)

`project_brief.md` names two categories of comparison directly:

- **Hospitality communication/guest-engagement platforms** (e.g. HiJiffy, Duve) — already offer
  omnichannel messaging, upsell, and guest analytics. Our stated opportunity is to extend past
  that into **experience quality and booking-influence metrics**, not just message volume.
- **Generic AI chatbots** — the ProblemSection copy names this directly: "robotic chatbot
  popups... miss context, break your brand voice, and turn a warm welcome into an IVR menu."
  Our differentiation is the storytelling/sensory response layer plus the grounded knowledge
  engine (verified-content-only, no hallucinated rates or availability).
- **Do not** position against OTAs (Booking.com, Agoda, Expedia) as competitors — they are
  integration partners and distribution channels holaa is designed to work alongside, with the
  explicit goal of increasing the *direct* share of that mix, not replacing OTA presence.
- **Website-widget-only competitors** — many hotel chatbot/concierge vendors, including several
  of the international platforms above, are reachable only via an embedded website widget.
  holaa's WhatsApp-native concierge and no-app in-room QR concierge (brand pillar 5, above;
  full detail in `hola_product_offerings.md` §2.6–2.7) are a genuine, demonstrable point of
  difference against that category — especially decisive for Sri Lankan hotels evaluating
  whether an AI concierge vendor actually understands how their guests and staff already
  communicate, versus a generic international tool retrofitted to the market.

---

## 9. Brand Pillars

1. **Grounded, never hallucinated.** Every AI answer traces back to hotel-verified content.
   This is a trust claim as much as a technical one — lead with it whenever accuracy or
   reliability is in question.
2. **Storytelling over spec sheets.** The sensory, experiential answer is the product's
   signature move. See `hola_brand_voice_guide.md` for exactly how this sounds in copy.
3. **An extension of the hotel's own team, not a vendor's bot.** Persona, tone, and greeting
   style are all hotel-configurable (see the Bot Persona Configuration Studio in
   `hola_product_offerings.md`) — the brand promise is that holaa disappears into the hotel's
   own voice, not the other way around.
4. **Direct revenue, plainly stated.** The business case is never abstract "engagement" — it's
   OTA commission avoided, direct bookings captured, *and* ancillary commission earned on
   partner experiences the AI surfaces (real per-experience revenue-attribution analytics exist
   — see `hola_product_offerings.md` §2.8). Copy should say so in numbers wherever real numbers
   are available, and should remember the business case isn't only about room revenue.
5. **Wherever the guest already is — no app, no friction.** holaa doesn't ask a guest to change
   their behavior to reach it: the same concierge is reachable on the hotel's website, on
   **WhatsApp** (a two-way conversation on the hotel's own number, plus a staff relay that
   routes service requests to the right team by category), and via a **scan-to-chat in-room QR
   code** that opens instantly in the guest's phone browser — no app download, no account. This
   is a materially real, shipped differentiator (see `hola_product_offerings.md` §2.6–2.7), and
   it's a particularly strong one in this market specifically: WhatsApp and QR-first digital
   habits are already the default for Sri Lankan and wider South/Southeast Asian leisure
   travelers, so this isn't a "nice extra channel" — for many prospects here, it's the reason
   holaa is credible where a website-widget-only competitor isn't.
6. **Honest feedback, not managed reputation.** The post-stay checkout QR survey
   (`hola_product_offerings.md` §2.9) captures specific, structured answers from every guest —
   not a generic star box — and turns them into an AI-drafted review the guest can post
   verbatim, with the *identical* flow shown to every respondent regardless of score. Never
   describe this as a way to filter or suppress negative feedback from reaching public review
   sites — that would misrepresent a real, deliberate design choice as the opposite of what it
   is. The honest framing ("more specific, not just more positive") is also the more credible
   one with GMs who've been burned by review-gating tools before.

---

## 10. Quick Reference Facts

- Tagline: **"Every great stay starts with a holaa."**
- Product philosophy line: **"Guests don't book rooms. They book experiences."**
- Contact used in demo CTAs: `concierge@holaa.com`
- Footer legal line (demo copy): "© holaa Hospitality Inc. All rights reserved." — confirm the
  real registered entity name with Legal before this leaves demo status.
- Brand mark: lowercase wordmark **"holaa"** with a smiley-face glyph replacing the second "o";
  a standalone waving-hand mark is used as an icon/favicon-scale alternate. Full usage rules in
  `hola_brand_style_guide.md`.

---

## 11. Related Documents

- **[[hola_product_offerings]]** — full feature inventory, prioritized
- **[[hola_brand_voice_guide]]** — how we sound
- **[[hola_brand_style_guide]]** — how we look
- **[[hola_growth_marketing_context]]** — GTM strategy, ICP detail, channel plan
- **[[sop_campaign_performance_reporting]]** — how we measure marketing performance
