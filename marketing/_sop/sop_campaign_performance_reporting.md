# SOP: Campaign Performance Reporting

**Owner:** Marketing
**Applies to:** All paid, organic, content, social, partnership, and outbound campaigns run
under the holaa brand.
**Related documents:** `hola_growth_marketing_context.md` (strategy this reporting measures
against), `hola_brand_context.md` §7 (what's real vs. placeholder — never report a placeholder
figure as an actual result), `hola_product_offerings.md` (feature/tier reference for
segmenting campaign performance by plan tier interest).

---

## 1. Purpose

Define a consistent, repeatable process for measuring, reporting, and acting on marketing
campaign performance — so results are comparable period over period, decisions are made from
the same numbers Sales/Finance trust, and underperformance is caught early enough to fix within
a campaign's flight, not just post-mortemed after it ends.

---

## 2. Reporting Cadence

| Cadence | Audience | Content |
|---|---|---|
| **Weekly** (every Monday, covering the prior Mon–Sun) | Marketing team | Channel-level pulse: spend, leads, demo requests, top/bottom performing campaigns. Fast, informal, catches problems early. |
| **Monthly** (first business week of the month, covering the prior calendar month) | Marketing + Sales + leadership | Full funnel report: acquisition by channel, cost per demo request, demo-to-close rate by channel/tier, content performance, campaign-level ROI. This is the report of record. |
| **Quarterly** (within 2 weeks of quarter close) | Leadership | Trend analysis, channel mix reallocation recommendation, ICP/positioning validation against actual closed-won deals, strategy adjustments to `hola_growth_marketing_context.md`. |
| **Ad hoc / campaign close-out** | Campaign owner + Marketing lead | Within 5 business days of any discrete campaign ending (a launch push, an event, a paid flight) — a dedicated close-out report (§5). |

---

## 3. The Funnel We Report Against

Matches `hola_growth_marketing_context.md` §6 — every report should be structured around these
stages, not an ad-hoc metric list:

```
Awareness → Problem Recognition → Product Reveal (interactive demo engagement) 
  → Proof (case study / pricing page engagement) → Demo Request (primary conversion event) 
  → Sales-Qualified → Closed-Won (by plan tier) → Expansion (tier upgrade / additional properties)
```

### 3.1 Core Metrics by Stage

| Stage | Primary metric | Secondary metrics |
|---|---|---|
| Awareness | Reach / impressions by channel | Content engagement rate, organic search impressions |
| Problem Recognition | Content page views (problem/OTA-commission content pillar) | Time on page, scroll depth |
| Product Reveal | Interactive demo engagement rate (site's live concierge simulator) | Demo interactions per session, prompts tried |
| Proof | Pricing page views, case study views | Return visits to pricing/proof pages |
| Demo Request | **Demo requests submitted** (primary conversion event — "Book a demo" CTA) | Cost per demo request, by channel |
| Sales-Qualified | SQL rate from demo request | Time-to-first-response |
| Closed-Won | Closed-won count and $ by plan tier (Starter/Discover/Engage/Inspire) | Sales cycle length, win rate by channel source |
| Expansion | Tier upgrades, additional properties added by existing customers | Expansion revenue by original acquisition channel |

**Primary north-star metric for all reporting: Demo Requests, segmented by source channel and
(once available) by eventual plan tier / closed-won outcome.** This is deliberately not raw
traffic or engagement — it mirrors the product's own internal discipline of measuring outbound
booking-intent and click-through rather than conversation volume (see
`hola_product_offerings.md` §3.9), and it's the metric that actually maps to pipeline.

---

## 4. Data Sources

| Data | Source of truth |
|---|---|
| Paid campaign spend/performance | Respective ad platform (confirm current platforms with Marketing lead — not yet standardized in this workspace) |
| Organic/SEO performance | Analytics platform + search console (confirm current tooling with Marketing lead) |
| Demo requests | CRM / inbox tracking `concierge@holaa.com` demo-request submissions and any dedicated demo-request form, once one exists beyond the current `mailto:` CTA |
| Sales pipeline / closed-won by tier | Sales/CRM system (source of truth for stage 3.1's Sales-Qualified through Expansion rows) |
| Social performance | Native platform analytics per channel |
| Content/SEO page-level engagement | Analytics platform |

**Note:** as of this document's authoring, the live site's demo CTA is a plain `mailto:` link
(`concierge@holaa.com`) rather than a trackable form — this is a gap worth flagging to
Product/Marketing leadership, since it limits attribution accuracy at the most important
funnel stage (Demo Request). Recommend prioritizing a trackable demo-request form as a
prerequisite for reliable channel-level ROI reporting.

---

## 5. Report Structure (Monthly & Campaign Close-Out)

Every report should follow this structure, in this order, so readers can compare period to
period without re-orienting:

1. **Headline summary** — 3–5 bullets, north-star metric first, plain language, no jargon.
2. **Funnel snapshot** — the §3 table populated with this period's numbers and period-over-
   period change.
3. **Channel breakdown** — performance by channel (paid, organic/SEO, content, social,
   partnership, outbound), each against its own cost-per-demo-request and demo-to-close rate
   where available.
4. **By plan tier** — which campaigns/channels are attracting interest that maps to which
   pricing tier (Starter through Inspire) — ties campaign performance back to
   `hola_product_offerings.md` §5 and the ICP table in `hola_growth_marketing_context.md` §2.
5. **Content/messaging performance** — which positioning pillars (per
   `hola_growth_marketing_context.md` §3) are resonating, measured by engagement and demo-
   request rate on the content built around each pillar.
6. **What changed and why** — any campaign launches, pauses, creative refreshes, or targeting
   changes made this period, and the rationale.
7. **Recommendation** — 1–3 concrete actions for next period (scale up, pause, reallocate
   budget, refresh creative, retarget ICP).

---

## 6. Data Integrity Rules

- **Never report a placeholder or illustrative figure as a real result.** If a report needs to
  reference pricing, always use figures confirmed with Finance/Sales, never the placeholder
  figures in `hola_product_offerings.md` §5 unless explicitly labeled as such.
- **Attribute by first-touch channel, report by both first-touch and last-touch** where the
  data source allows it — a report that only shows last-touch will systemically undercredit
  awareness-stage content.
- **Reconcile demo-request counts against Sales' own logged count monthly** — if Marketing's
  tracked demo requests and Sales' logged inbound leads diverge by more than ~10%, treat it as
  a tracking-gap incident, not a real performance signal, and fix attribution before drawing
  conclusions from that period's numbers.
- **Flag any campaign or asset that uses `[ILLUSTRATIVE]`/`[PLACEHOLDER]` content** (per
  `hola_brand_context.md` §7) in the report itself, so leadership knows performance is being
  measured on demo/placeholder creative, not final assets, where applicable.

---

## 7. Roles & Responsibilities

| Role | Responsibility |
|---|---|
| **Campaign owner** | Owns weekly pulse-check on their own campaign(s); submits campaign close-out report within 5 business days of campaign end. |
| **Marketing lead** | Compiles and distributes the monthly funnel report; owns the quarterly trend/strategy review; escalates data-integrity issues (§6). |
| **Sales liaison** | Provides closed-won/tier/sales-cycle data monthly; participates in the monthly report review to validate demo-to-close numbers. |
| **Leadership** | Reviews monthly and quarterly reports; approves channel mix/budget reallocation recommendations. |

---

## 8. Escalation

If a campaign's cost-per-demo-request exceeds 1.5x the trailing-3-month channel average, or a
channel's demo-to-close rate drops by more than 30% relative to its own trailing average, the
campaign owner flags it in that week's pulse-check (not held for the monthly report) and
proposes a pause/adjust/continue recommendation to the Marketing lead within 3 business days.

---

## 9. Related Documents

- **[[hola_growth_marketing_context]]** — the strategy this SOP measures performance against
- **[[hola_brand_context]]** — source of truth for what's real vs. placeholder/illustrative
- **[[hola_product_offerings]]** — plan-tier reference for funnel segmentation
