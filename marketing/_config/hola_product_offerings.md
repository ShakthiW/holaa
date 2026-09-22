# holaa — Product Offerings

**Status:** Reference document. This is the ground-truth feature catalog — cross-checked
against actual source code (`chatbot-demo-admin`), not just the marketing site's own copy.
Anything below marked `[UNVERIFIED]` or `[ROADMAP]` should not be sold or promised as a
current, working capability without Product/Engineering sign-off. See §0 for how this document
was assembled and `hola_brand_context.md` §7 for the full real-vs-illustrative reconciliation.

**Revision note (rev. 2):** the first pass of this document under-weighted four real,
shipped capabilities that were flagged internally as genuine difference-makers versus
competitors — all four are now Tier 1: the WhatsApp guest concierge & staff relay (§2.6), the
in-room QR concierge (§2.7), the Experience Upsell Engine with real partner commission tracking
and revenue attribution (§2.8), and the post-stay checkout QR survey that turns structured
answers into AI-drafted public reviews (§2.9). The WhatsApp and QR-concierge pieces are
particularly strong in the Sri Lankan and wider South/Southeast Asian market, where WhatsApp-
and QR-first, no-app-required guest habits are already the norm.

---

## 0. How This Document Is Organized, and Why

Every capability below is prioritized and ranked into three tiers — **Tier 1: Lead With This**,
**Tier 2: Strong Supporting Proof**, **Tier 3: Roadmap / Use Sparingly** — based on three
criteria: (a) how directly it drives the core business outcome (direct bookings, OTA
commission avoided), (b) how differentiated it is versus the named competitive categories in
`hola_brand_context.md` §8, and (c) how solid the evidence is that it's actually shipped and
working today. This ranking is my own synthesis from the codebase research — treat it as a
starting recommendation for Sales/Marketing prioritization, not a fixed hierarchy.

---

## 1. Platform Overview

holaa is a multi-agent AI concierge platform for hotels, delivered as:

1. A **guest-facing AI concierge** — reachable on the hotel's website (embeddable widget),
   WhatsApp, in-room via QR code, and through a post-stay survey flow — that answers questions
   with grounded, storytelling responses and renders rich interactive cards instead of plain
   text.
2. A **hotel staff admin dashboard** — the operational control centre for configuring the AI,
   managing property content, reviewing conversations, taking over chats live, and tracking
   booking-intent analytics.

Both are powered by a shared multi-agent AI architecture and a per-property knowledge base, so
what staff upload in the dashboard is what the AI can (and only can) talk about.

---

## 2. Tier 1 — Lead With This (Core Differentiators)

### 2.1 The Storytelling & Sensory Experience Engine
**The single biggest differentiator, per our own internal audit.** Instead of answering "What's
the Ocean View Suite?" with square footage, the AI answers the emotional question: *"Around
sunrise you'll usually hear the waves before you see them..."* This is structurally built in —
every `RoomType` carries a dedicated `sensory_experience` field, and the AI's response-detail
level (`rich` / `balanced` / `concise`) is hotel-configurable. This is the feature that makes
holaa read as "a concierge," not "a chatbot," and should anchor almost every piece of top-of-
funnel messaging.

### 2.2 The Grounded Knowledge Engine (RAG, verified-content-only)
A Retrieval-Augmented Generation pipeline (Qdrant vector search + Gemini embeddings) that
indexes a hotel's own uploaded documents — PDFs, menus, policies, room descriptions, past-guest
survey feedback — and answers *only* from that verified content. This is the trust claim that
neutralizes the single biggest objection prospects will raise about any AI concierge:
hallucinated rates, invented amenities, or off-brand answers. Several tools have hard,
code-level refusals against inventing data (e.g. the dining-menu tool will say a menu isn't
configured yet rather than fabricate dishes) — this is a real, demonstrable safety property,
not just a marketing line.

### 2.3 Generative UI — Rich Interactive Cards, Not Chat Bubbles
21 purpose-built React components (room carousels, comparison tables, dining menus, spa
treatment cards, itinerary timelines, booking-hold countdowns, payment checkout cards, weather
cards, and more) render inline in the conversation, driven by real backend tool calls rather
than canned templates. This is a strong, visually demonstrable differentiator in any demo —
show, don't just tell.

### 2.4 Multi-Agent Architecture (Concierge / Booking / Dining & Spa / Itinerary)
A LangGraph-orchestrated system with four specialized sub-agents and a supervisor router that
hands conversations off seamlessly (a guest asking about rooms mid-itinerary-planning gets
routed to the Booking agent without a jarring restart). Each sub-agent has its own persona and
tool palette, so answers stay in-scope and high-quality. This is a strong technical proof point
for buyers evaluating "is this a real product or a wrapped prompt" — useful in sales
engineering conversations, secondary in top-of-funnel copy (it's an architecture detail, not an
emotional hook).

### 2.5 Direct-Booking-First Omnichannel Distribution
A 4-tier destination-resolution system (room-level override → property preferred channel →
automatic OTA deep-link fallback → inquiry modal) routes every guest booking intent to the
hotel's preferred channel, with full outbound-click tracking and per-room CTR analytics in the
dashboard. This is the mechanism behind the OTA-commission-avoidance pitch — it's concrete and
measurable, not just a slogan.

### 2.6 WhatsApp-Native Concierge & Staff Notification Relay
**This was under-highlighted in earlier drafts of this document — it belongs in Tier 1.** It's
real, live, shipped in production depth (not a thin webhook demo), and it's a genuine
category-defining advantage in markets — Sri Lanka very much included — where WhatsApp is
already how guests and hotel staff communicate by default. Two genuinely separate subsystems,
both running on one connected hotel WhatsApp number:

- **Guest-facing concierge (two-way).** A guest messages the hotel's own WhatsApp number, or
  taps a Click-to-WhatsApp ad, and holds a real conversation with the **exact same LangGraph
  agent** that powers the web widget — same router, same 15 tools, same entitlement rules, zero
  separate "WhatsApp bot" logic to fall out of sync. Generative-UI card payloads degrade
  gracefully into WhatsApp-native image messages (room photos, dining/spa item photos, each
  captioned "Name — Price," capped at 5 images per reply) with the AI's own text closing the
  reply — guests get a genuinely rich experience without a chat widget or app at all.
- **Staff notification relay (outbound).** Guest service requests (housekeeping, room service,
  spa booking, general inquiries) route automatically, by category, to the right configured
  staff phone or WhatsApp group — hotel managers pick real WhatsApp groups from a live list
  rather than typing a phone number blind. A slow or failed relay never blocks or fails the
  guest's own request (fire-and-forget dispatch).
- **Real production hardening, not a demo integration:** HMAC-signed webhook verification,
  SSRF-guarded callback registration, per-guest rate limiting (soft-cap warning + hard-cap
  silent drop), per-thread message serialization (prevents two concurrent messages from the
  same guest corrupting one conversation's state), and self-healing session reconnection if the
  WhatsApp gateway session drops. This level of engineering rigor is a legitimate talking point
  with technically sophisticated buyers (hotel groups, IT-literate GMs) — it signals this isn't
  a fragile weekend integration.
- **Live human handover works on WhatsApp too** — on plans with live handover, staff can take
  over a WhatsApp conversation from the dashboard exactly as they would a web chat, and the AI
  automatically stops responding until handed back.
- **Precision note:** built on a self-hosted OpenWA gateway (`whatsapp-web.js`/`baileys`), not
  Meta's official WhatsApp Business Cloud API — say "WhatsApp concierge" or "guest WhatsApp
  messaging" in technical/precise contexts (see `hola_brand_voice_guide.md` §4). This doesn't
  weaken the pitch — it's a real, working two-way integration either way — but don't claim the
  official API by name.
- **Known gaps, worth knowing before a technical buyer asks:** no dedicated Social Inbox UI yet
  for resuming a muted (handed-over) WhatsApp session — it requires a direct staff API call
  today; conversation retention/summarization is designed but not yet implemented (every thread
  accumulates state indefinitely); `SendLocation`/`SendContact`/`SendPoll` are not implemented,
  so those payload types fall back to plain text.

### 2.7 In-Room QR Concierge — No App Required
A second real, shipped, and genuinely differentiated guest touchpoint: every room gets a
unique, downloadable, print-ready QR code (generated from the Rooms admin page) that opens a
**full-screen, room-context-aware version of the same AI concierge** directly in the guest's
phone browser — no app download, no account, no login. The card's own on-product copy states
the pitch better than we could: *"Scan to chat with your concierge — in-room dining, spa
booking & guest services 24/7 — no app download required."*

- Because it's room-scoped (`/q/{propertyId}/{roomId}`), the concierge opens already knowing
  which room the guest is in — a materially better starting point than a generic front-desk
  chat widget.
- Staff download a branded, print-ready QR card per room (hotel name, room name/code, QR code,
  call-to-action copy) directly from the dashboard, or copy the raw guest link, or test it live
  — zero engineering involvement needed to roll this out room-by-room.
- This is one of the platform's lowest-friction guest touchpoints to demo and to sell: a GM can
  literally scan a code on their own phone during a sales call and be in a live conversation
  about their own hotel in seconds.
- **Why this matters more in this market specifically:** guest willingness to download a
  dedicated hotel app is low almost everywhere, and Sri Lankan and wider South/Southeast Asian
  leisure travelers skew heavily toward WhatsApp and QR-first digital habits already — a
  no-app, scan-to-chat concierge meets guests exactly where their behavior already is, which is
  a real adoption advantage over competitors whose only guest entry point is a website widget.

### 2.8 Experience Upsell Engine — Partner Commission & Revenue Attribution
**Also under-highlighted in the first pass of this document — this is a real, fully-built
ancillary-revenue engine, not just "nice recommendations."** Hotel staff manage a single
catalog of in-hotel activities, curated **partner experiences**, and local attractions in a
dedicated dashboard section (the "Guest Experience Engine," `/dashboard/experience`) — and that
same catalog is the *one shared source of truth* the AI itinerary generator and guest chat
concierge both read from, so what staff configure is exactly what guests get offered.

- **Real commission economics, not just a recommendation.** Every partner experience carries
  its own **guest discount percentage** and **hotel commission percentage** as first-class
  fields — this is a genuine revenue-share upsell mechanic (a local diving tour, a tea-estate
  tasting, a sunset cruise booked through the AI earns the hotel a commission), not a vague
  "personalized suggestion" claim.
- **Surfaced with context, not as a banner ad.** The itinerary generator weaves partner
  experiences into a guest's personalized day-by-day plan alongside hotel outlets and
  destination attractions, each visibly source-badged ("Hotel Featured" / "Must See" / "Partner
  Discount") so the guest always knows what they're looking at — see
  `hola_product_offerings.md` §3.2 for the itinerary mechanic itself.
- **Item-level upsell inside dining and spa, too.** Dishes and treatments carry a real,
  backend-driven "chef recommendation" / "signature therapy" flag that the generative-UI cards
  (`DiningMenuUI`, `DishDetailUI`, `SpaTreatmentUI`, `TreatmentDetailUI`) visibly highlight —
  a simple, real lever for hotels to nudge guests toward higher-margin dishes and treatments
  without any extra engineering.
- **Real attribution analytics, matching the depth of the booking-click analytics in §2.5.**
  Per-experience and property-wide metrics — impressions, detail views, bookings,
  **revenue influenced**, conversion rate, and average rating — are tracked and queryable
  (`/api/v1/properties/{id}/experiences/analytics`). This is a strong, concrete proof point for
  revenue-minded buyers: the platform doesn't just claim it drives ancillary revenue, it
  measures and reports the number.
- **`[CAVEAT]`** the `experiencesEnabled` per-tier entitlement flag exists in the backend
  entitlement schema (and is listed as an Engage-tier feature in the pricing copy, §5), but a
  code audit found no place where that flag is actually checked to gate access to the
  Experience Engine dashboard page or the itinerary tool — unlike `itineraryEnabled`, which
  **is** actively checked by the AI router. Treat "Curated experiences & partner marketplace"
  as a real, working *feature*, but don't assume the plan-tier gate around it is technically
  enforced yet without confirming with Engineering — worth flagging internally, not a reason to
  undersell the feature itself.
- **`[DO NOT CONFUSE WITH]`** the AI's separate, spontaneous single-item recommendation tool
  (`get_personal_recommendation`, rendered as `PersonalRecommendationUI`) is, today, a
  **hardcoded static demo payload** — it always returns the same fixed "Beachfront Plunge Pool
  Villa" recommendation regardless of the guest's actual stated preferences. It's real UI, real
  plumbing, and a real tool the agent can call — but the recommendation logic itself isn't yet
  wired to real guest data or the Experience Engine catalog. Don't describe this specific tool
  as "AI-personalized upselling" until that wiring is real; the Experience Engine and itinerary
  generator above are the parts of this story that are fully real today.

### 2.9 Post-Stay Checkout QR Survey — Structured Feedback, Not Generic Star Ratings
A second real, shipped QR touchpoint distinct from the in-room concierge (§2.7): a
**post-stay guest survey**, designed explicitly to be placed "at the checkout desk, on a room
card, or on the receipt" (the product's own in-app guidance) — a guest scans it on the way out
and answers in under a minute.

- **Structured question types, hotel-configurable per survey:** NPS (0–10), star rating (1–5),
  multiple choice, and free text — built with a dashboard survey builder, not a single generic
  "how was your stay?" box.
- **The genuinely differentiated part: it drafts the public review *for* the guest, from their
  own structured answers.** On submit, the platform composes an AI-written review from what the
  guest actually said, and gives the guest one-tap links to paste it straight into Google,
  TripAdvisor, or Agoda. This is the concrete answer to "how is this better than generic
  feedback tools" — instead of hoping a guest bothers to write a thoughtful public review from
  scratch (most don't, and the ones who do are disproportionately the unhappy ones), holaa
  turns a guest's own quick structured answers into a specific, genuine-sounding, ready-to-post
  review the guest just has to approve and paste.
- **Ethically even-handed, not a reputation-gating dark pattern:** every respondent sees the
  identical "thank you" and review-sharing flow regardless of their score — there's no hidden
  branch that quietly suppresses unhappy guests from reaching public review sites while pushing
  happy ones. This is worth stating plainly to a skeptical buyer (or a journalist) — it's a
  meaningful, checkable trust point, not spin.
- **The structured answers feed the hotel's own operations, not just public reviews.** Responses
  generate internal staff notifications and become part of the property's searchable knowledge
  base (the RAG knowledge engine's tools explicitly cite "real past-guest feedback" as a
  retrieval source) — meaning a *future* guest's question can be answered informed by what
  *previous* guests actually said, not just brochure copy.
- **Anonymous by default** — name and room number are both optional, clearly labeled "leave
  blank to stay anonymous."
- **Zero-cost, zero-risk preview mode for staff:** managers can run the exact same guest flow
  from the builder to test a survey (including an unpublished draft) with no data saved, no AI
  spend, and no staff notification triggered.

**Positioning line worth reusing directly:** *"Meaningful feedback, not generic stars — guests
tell us what actually happened, and we turn it into the review they were always going to write
anyway, just faster and more specific."*

---

## 3. Tier 2 — Strong Supporting Proof

### 3.1 Destination & Local Experience Intelligence
Beyond the hotel itself, the AI answers questions about the surrounding destination —
attractions, best visiting times, transport, hidden local spots — turning it into a trusted
travel companion, not just a property FAQ. (Built and demonstrated Sri Lanka-first: temple
visits, tea estate tours, whale-watching seasons, surf breaks — but the underlying data model
is destination-agnostic and reusable for any property.)

### 3.2 AI Itinerary Generator
Guests provide trip length, travel style (romantic/family/active/wellness/luxury), interests,
and budget; the AI weaves hotel outlets, destination attractions, and partner experiences into
a day-by-day plan with time-of-day scheduling logic (sunrise activities early, spa in the
midday heat, sunset/dinner in the golden hour). Entitlement-gated — only live on Discover tier
and above.

### 3.3 Hour-by-Hour Experience Timeline
A sensory "day in the life of your stay" preview (what's the beach like at sunset, when is the
pool quiet) — directly answers the emotional pre-booking questions named in the Problem
Statement (`hola_brand_context.md` §4). Pairs naturally with the Itinerary Generator in a demo
narrative: "see what a day looks like, then plan several."

### 3.4 Dual-Tier Guest Memory
Short-term session memory (preferences extracted live, zero added latency) plus long-term
cross-session guest profiles for returning guests — "Welcome back, the Ocean View Suite has
been reserved for you again." Strong in a loyalty/repeat-guest narrative; less useful as a
first-touch hook since prospects can't experience it in a single demo session.

### 3.5 Bot Persona Configuration Studio
Property-configurable persona presets (luxury / island host / heritage / modern), response
detail, greeting style (including a Sri Lankan `ayubowan` traditional-greeting preset), and a
guardrail strictness setting. This is the "it becomes *your* concierge, not a vendor's bot"
proof point — pairs with brand pillar 3 in `hola_brand_context.md`.
`[NOTE]` the multi-select "personality traits" picker in this same panel is UI-only and not
yet persisted server-side — don't promise trait-level tuning specifically; `tone_preset`,
`response_length`, and `greeting_style` are the settings that actually take effect.

### 3.6 Seasonal Intelligence & Pricing Context
The AI explains *why* a date is priced the way it is ("December is peak whale-watching season,
that's why rates are higher — a week later is nearly identical for less"). This reframes price
objections into value understanding rather than sticker shock — a genuinely useful sales-enablement
angle for the hotels themselves to use with their guests.

### 3.7 Heritage Story Builder
Hotels upload history, local legends, chef stories, architecture, and sustainability
narratives; the Concierge sub-agent weaves them into relevant conversations automatically. Good
supporting proof for boutique/heritage-property prospects specifically — less relevant for a
large chain pitch.

### 3.8 Hotel Operations Dashboard
The staff-facing control centre — property content management (rooms, outlets, media, stories,
attractions, seasons, events), a **Quick Ingest** flow (6-category structured knowledge
ingestion, plus raw PDF/TXT/MD upload) for fast knowledge-base setup, live conversation review
with a dedicated **WhatsApp social inbox**, a **live human handover / takeover** flow, and a
**Playground** for staff to test the AI before guests do. This is the operational proof point
for the buyer persona (a GM/owner who needs to trust they can actually run this) — strong in a
demo, secondary in acquisition copy.

### 3.9 Analytics & Token Telemetry
Outbound booking-intent analytics (click-through by room, by channel) plus real-time multi-
tenant AI usage/token telemetry with monthly automated resets and threshold warnings (80% /
100% of quota). Genuinely differentiated depth of observability for this product category —
useful in the Engage/Inspire sales conversation, where buyers are more sophisticated about
usage-based cost.

### 3.10 Digital Concierge Studio (widget branding, zero-code)
A live-preview visual editor for the embeddable web widget's branding, imagery (including
crop/framing controls), concierge identity, and copy — plus a "Brand Import" tool that pulls
brand colors/style from a URL. Good self-serve/low-friction onboarding story.

---

## 4. Tier 3 — Roadmap / Use Sparingly (Confirm Before Promising)

These appear in our own marketing copy or vision docs but are **not verified as shipped** in
the current codebase. Use only as "on our roadmap" framing, never as a current capability, in
any external-facing material:

- **Voice Concierge** — natural spoken interaction. No voice code found anywhere in the app
  despite appearing in the landing page's own feature grid. `[ROADMAP]`
- **Hotel Digital Twin** — interactive 3D/spatial property exploration. No implementation
  found. `[ROADMAP]`
- **Computer Vision Search** ("show me a room like this photo"), **AR Hotel Guide**,
  **Predictive Hospitality AI**, **Cross-Hotel Network Intelligence**, **Sustainability
  Assistant**, **Experience Marketplace** — all explicitly listed as "Future Roadmap" in
  `project_brief.md`. `[ROADMAP]`
- **Omnichannel beyond WhatsApp + web widget** — Facebook Messenger, Instagram DMs, kiosks,
  reception tablets, voice assistants are named in `platform_features.md`'s "Omnichannel
  Deployment" section, but only WhatsApp, the embeddable web widget, in-room QR ordering, and
  post-stay surveys are live channels today. `[ROADMAP]` for the rest.
- **Live 2-way PMS inventory sync / "instant 15-minute room holds" as the default guest
  experience** — V1 ships in **External Booking Engine Mode**: holaa routes guests to the
  hotel's existing booking engine or OTA rather than holding real-time inventory by default.
  The 15-minute hold + payment-link checkout flow exists and works, but is the "Integrated
  Mode" path for future/selected live-PMS deployments, not the default V1 flow. `[UNVERIFIED
  as default]`
- **AI Feedback Console / continuous learning loop** — the dashboard page for this runs on
  hardcoded mock data and is labeled in-app as a placeholder awaiting a real backend. Don't
  describe a live "approve/improve/retrain" feedback loop as working today. `[NOT REAL]`
- **45+ language support, SOC2 Type II certification, GDPR/CCPA compliance, AES-256
  encryption, "native 2-way API connectors" for Opera/Cloudbeds/Mews with sub-48-hour setup** —
  all stated on the live marketing site's FAQ, none independently verified against code or a
  compliance artifact during this research pass. Flag to Legal/Security/Product for
  confirmation before repeating in any sales, compliance, or RFP context. `[UNVERIFIED]`
- **"WhatsApp Business API"** — the integration is real and working, but built on a self-hosted
  OpenWA gateway (`whatsapp-web.js`/`baileys`), not Meta's official Cloud API. Say "WhatsApp
  concierge" or "guest WhatsApp messaging" in precise/technical contexts; reserve "WhatsApp
  Business API" for looser marketing copy only if Legal is comfortable with the imprecision.

---

## 5. Pricing & Packaging

`[PLACEHOLDER PRICING — confirm with Finance/Sales before external use]`

| Plan | Price (placeholder) | Segment | What's added over the previous tier |
|---|---|---|---|
| **Starter** | $190/mo (annual) · $230/mo | Single property, finding its feet | AI concierge + booking assistant, ≤20 knowledge base documents, standard AI model tier, web widget, email & chat support |
| **Discover** | $490/mo (annual) · $590/mo | Boutique hideaways & lodges | + AI itinerary generator, full guest memory/intelligence, in-room QR codes & widget, ≤75 knowledge base documents |
| **Engage** ⭐ most popular | $990/mo (annual) · $1,190/mo | Luxury resorts & ocean villas | + Multichannel/OTA distribution, curated experiences & partner marketplace, full revenue analytics dashboard, upgraded ("Pro") AI model tier, ≤300 knowledge base documents |
| **Inspire** | Custom | Enterprise hotel collections | + Live human handover to front desk, frontier AI model tier, unlimited knowledge base documents, priority support & onboarding |

**WhatsApp entitlement** (`whatsapp_enabled`, per the backend entitlement system): included by
default on **Engage and Inspire**; available as a **purchasable add-on on Starter and
Discover**. This is a real, verified entitlement gate — worth leading with in sales
conversations for Starter/Discover prospects specifically, since "WhatsApp concierge" (§2.6) is
one of the strongest differentiators in this document and shouldn't be assumed Engage-tier-only.

The tier boundaries themselves (which features gate at which level) **are real** — they trace
to an actual entitlement-flag system in the backend (`resolveConciergeEntitlements`:
`itineraryEnabled`, `experiencesEnabled`, `liveHandoverEnabled`, `multichannelEnabled`,
`modelTier`), fails closed on error, and is what the AI router itself checks before offering
itinerary planning, for example. **Only the dollar figures are placeholder** — treat the
feature-gate structure as trustworthy, the prices as not-yet-final.

---

## 6. Integrations

| Partner | Category | Status |
|---|---|---|
| WhatsApp (self-hosted OpenWA gateway) | Guest messaging | **Live, Tier 1 differentiator** — two-way guest concierge + staff notification relay, production-hardened. Full detail in §2.6. |
| Oracle Opera PMS, Cloudbeds, Mews | PMS | Adapter architecture exists; depth of live sync `[UNVERIFIED]` in this codebase — likely deeper in the separate backend repo, confirm before quoting setup timelines |
| Booking.com, Agoda, Expedia | OTA distribution | Live at the *routing/deep-link* layer (4-tier destination resolver with affiliate parameter injection); full 2-way channel-manager sync `[UNVERIFIED]` |
| Stripe | Payments | Referenced in integration copy; payment-link/checkout flow exists in the booking tool chain — confirm live processing status with Engineering before quoting |
| Google Calendar | Concierge scheduling | Referenced in marketing copy; not confirmed in this codebase — `[UNVERIFIED]` |
| Custom GraphQL API | Developer SDK | Referenced in marketing copy; not confirmed in this codebase — `[UNVERIFIED]` |

---

## 7. The Admin Dashboard — Full Section List

For sales engineering / demo scripting purposes, the real dashboard sections are: Overview,
Rooms (+ per-room QR codes, §2.7), Outlets, Stories, Attractions, **Experience** (the Guest
Experience Engine — in-hotel activities, partner experiences with commission tracking, and
local attractions, §2.8), Seasons, Events, Knowledge (+ Quick Ingest), Media, Bot Config /
Settings (Persona & Behavior), Bookings, Requests, Guests, Analytics, Telemetry, Playground,
Widget / Digital Concierge Studio, Social Inbox (WhatsApp), Conversations (+ live takeover),
Notifications, **Surveys** (builder + per-survey QR codes, §2.9), Integrations, Profile.

`[NOTE]` `/dashboard/bot-config` and `/dashboard/takeover` are redirects into Settings and
Conversations respectively, not separate features — don't list them as distinct dashboard
sections in a feature count. `/dashboard/widget` and `/dashboard/studio` currently render the
same underlying editor. `/dashboard/packages` exists as an empty route with no page — not a
real, usable feature.

---

## 8. Related Documents

- **[[hola_brand_context]]** — positioning, ICP, the real-vs-illustrative reconciliation this
  document builds on
- **[[hola_growth_marketing_context]]** — how to turn this catalog into a GTM and messaging plan
- **[[hola_brand_voice_guide]]** / **[[hola_brand_style_guide]]** — how to talk about and show
  these features on-brand
