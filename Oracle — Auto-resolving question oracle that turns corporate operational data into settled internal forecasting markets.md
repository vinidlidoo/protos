---
id: proto-oracle
aliases:
  - Oracle
tags:
  - proto
type: proto
status: drafted
created: 2026-05-04
origin: ""
proto_generator:
  seed: 546011659
  writer: 1
  writers_total: 1
  repo_sha: b5b95f8
  generated_at: 2026-05-04T21:17:38+00:00
---

# Oracle — Auto-resolving question oracle that turns corporate operational data into settled internal forecasting markets

## What is it?

**Elevator pitch.** A platform-neutral settlement layer for corporate forecasting markets, grounded in the customer's own systems-of-record. RevOps and strategy teams pay Oracle to convert fuzzy operational questions ("Will the Q3 product launch ship by September 30?", "Will Enterprise ARR exceed $42M this quarter?") into machine-checkable contracts that auto-resolve against Jira, Salesforce, NetSuite, GitHub, or Looker — wherever the truth actually lives. The market platform itself (Manifold private, Polymarket-API, Anthropic-style internal, on-prem) is interchangeable; we own the question, the settlement, and the audit trail. That's the position no exchange-side incumbent can take without abandoning their own platform's neutrality, which is why this is structurally not Polymarket-Dome's wedge or Manifold's.

**How it works.** A user pastes a draft question; Oracle proposes a structured contract — outcome variable, source-of-truth system, query, settlement window, dispute window — and a calibrated tightening of the question text. Oracle holds read-only OAuth scopes into the customer's tools, polls the resolution query at the cutoff, posts the binary outcome on-chain or to the customer's chosen market platform via API, and signs the resolution receipt. The customer keeps the market wherever they already run it; Oracle owns the contract template library, the source-system connectors, and the audit trail.

## What's the problem?

Two decades of corporate prediction-market literature converge on one finding: managers do not adopt these markets because question-design and resolution are unsolved. Bo Cowgill's Google/Ford/Firm-X study showed corporate markets reduce expert forecast error by up to 25% MSE [(Cowgill & Zitzewitz)](https://funginstitute.berkeley.edu/wp-content/uploads/2014/04/CorporatePredictionMarkets1.pdf). Yet Google killed Prophit, restarted as Gleangen, and still struggled to "operationalize the wisdom of Googlers" — the LLM forecasting contest asked the wrong questions, framing internal milestones instead of competitor moves [(Asterisk)](https://asteriskmag.com/issues/08/the-death-and-life-of-prediction-markets-at-google). On Manifold today the resolution model is "whoever created the market gets to resolve it" [(Manifold FAQ)](https://docs.manifold.markets/faq) — fine for play; fatal in a corporate setting where bettors are subordinates of the resolver. The result: managers default back to the polling-optimists CRM forecasts that miss by >10% in 79% of B2B sales organizations [(Forecastio)](https://forecastio.ai/blog/sales-forecasting-accuracy-and-analysis).

## Why now (2026)

- **Public prediction markets just crossed institutional scale, normalizing the asset class for procurement.** Kalshi raised $1B at $11B in December 2025 and is now clearing >$1B per *week* in volume, up >1000% YoY [(Kalshi)](https://news.kalshi.com/p/kalshi-11-billion-valuation-series-e). When the head of Strategy googles "prediction market" she lands on an asset class respectable enough to write a memo about — not gambling.
- **A frontier AI lab launched an internal market with explicit decision-maker focus.** Anthropic technical-staff member Keri Warr announced at the 2024 Manifest conference that Anthropic had launched an internal prediction market with a "focus on decision-makers" — explicitly framed as a tool for executives rather than an HR engagement toy [(Asterisk)](https://asteriskmag.com/issues/08/the-death-and-life-of-prediction-markets-at-google). The reference customer for "well-run AI lab uses prediction markets" exists and is named.
- **Polymarket bought the unified API layer (Dome) in February 2026, signaling the infrastructure-not-frontend bet.** The acquisition rolls up the developer surface across Polymarket and Kalshi and signals that the next layer of value is *plumbing* — APIs, integrations, contract design — not yet another consumer market UI [(The Block)](https://www.theblock.co/post/390546/polymarket-buys-fresh-prediction-market-api-startup-dome-marking-second-official-acquisition).
- **LLMs make question-tightening cheap enough to ship as software for the first time.** Question design — "is this binary? auditable? what data resolves it?" — was the bottleneck a human consultant solved at $300/hr in 2015. In 2026 a frontier model can propose 90% of the contract structure given a draft and read access to the customer's data sources, with the human-in-the-loop only adjudicating edge cases.
- **LLM-driven forecasting research has flipped from "AI replaces the crowd" to "AI augments the crowd."** A June 2024 paper from DeepMind and the Google Gleangen team compared PaLM 2 forecasts to human Gleangen bettors and found AI is much better than chance but still meaningfully behind a human crowd [(Asterisk)](https://asteriskmag.com/issues/08/the-death-and-life-of-prediction-markets-at-google) — which means the buyer's choice is not "human market vs AI forecaster" but "human market resolved well + AI augmentation," exactly the resolvability surface Oracle owns.

## Who else is doing this

- **Cross-platform prediction-market API layers** — main player: **[Polymarket-Dome](https://www.theblock.co/post/390546/polymarket-buys-fresh-prediction-market-api-startup-dome-marking-second-official-acquisition)** (Polymarket's Feb-2026 acquisition of YC F25's Dome, a $4.7M-seed unified API across Polymarket and Kalshi). The closest comp on paper. The wedge is asymmetric: Dome unifies *exchange-side* APIs (market odds, order books, trades) for traders/devs building bots, dashboards, and trading tools that span Polymarket and Kalshi. Oracle unifies *settlement-side* contracts keyed to customer-side systems-of-record (Salesforce, Jira, NetSuite) for RevOps/CFO-budget buyers running internal markets. Dome's natural roadmap is sports/macro/political markets and trader tooling; absorbing Oracle's wedge would require Polymarket to (a) build privileged read access into customers' enterprise SaaS — a different product, GTM, and security posture, and (b) abandon platform neutrality, since Polymarket-owned Dome can't credibly settle markets onto a Kalshi or Manifold private instance. Distribution partner more naturally than competitor.
- **Public prediction-market platforms** — main player: **[Kalshi](https://news.kalshi.com/p/kalshi-11-billion-valuation-series-e)**. Others: [Polymarket](https://www.theblock.co/post/390546/polymarket-buys-fresh-prediction-market-api-startup-dome-marking-second-official-acquisition). They sell exchanges and matching engines for public markets. Internal/corporate versions are afterthoughts; resolution is creator-discretionary or oracle-disputed; none integrates with the customer's systems-of-record. Distribution partners, not competitors.
- **Internal prediction-market software** — main player: **[Manifold](https://docs.manifold.markets/faq)** (whose creator-resolves model is the public-market default). Others: built-in-house at Anthropic, Google's Gleangen [(Asterisk)](https://asteriskmag.com/issues/08/the-death-and-life-of-prediction-markets-at-google). They ship the market UI for a private group. They do not solve question-design or auto-resolution, which is the actual bottleneck.
- **AI-driven sales-forecasting tools** — main players: **[Forecastio](https://forecastio.ai/blog/sales-forecasting-accuracy-and-analysis)**, Clari, Gong RevOps, BoostUp. They predict revenue from CRM hygiene + ML on deal signals. They replace the analyst's spreadsheet, not aggregate distributed information from employees. Different mechanism, partially overlapping buyer (CRO).
- **Enterprise voice-of-customer / employee survey tools** — Glint, Lattice, Microsoft Viva. They collect opinion via Likert scales without skin in the game. The Cowgill/Zitzewitz study showed corporate prediction markets reduce expert-forecast error by up to 25% MSE [(Cowgill & Zitzewitz)](https://funginstitute.berkeley.edu/wp-content/uploads/2014/04/CorporatePredictionMarkets1.pdf) — different mechanism than survey instruments, complementary buyer (Chief People Officer).

**Where the opening is.** The strongest defensive insight is the same as the elevator pitch: this is a **cross-platform settlement layer keyed to the customer's systems-of-record** — owned by RevOps/CFO budget, not by exchange-side traders. Polymarket-Dome covers the trader-facing half of "unified API" and was built for it; absorbing the customer-side half would force them to abandon the neutrality their own platform depends on. Manifold's product instinct is to let the creator resolve. Anthropic built an internal-only system with no GTM. None of them naturally extends to "auto-resolve Acme Corp's Q3 launch market against Acme's Jira instance, regardless of which market platform Acme runs." The defensible play is the contract-template library + connector library + an AI-native question critic — deliberately platform-agnostic so any corporate-market platform (Manifold's private offering, a Polymarket-API private channel, an on-prem instance, a homegrown UI) can run on top.

## Why us

- **Vincent ran AI model evaluations at Amazon — calibration measurement and resolvability of a subjective question are the eval-engineering muscle.** "Did this output pass" decomposes the same way "did this market resolve YES" does: source-of-truth definition, ambiguity removal, edge-case adjudication. The skill that builds an LLM eval rubric *is* the skill that designs an auto-resolvable market contract; few founders in the prediction-market space have spent years doing it at production scale.

## Customer & buyer

- **Customer:** RevOps lead, Chief of Staff to a VP, or strategy-team analyst who already runs internal forecasting and is dissatisfied with the polled-optimists CRM forecast.
- **Buyer:** VP RevOps, CFO, or VP Strategy. Budget line: forecasting-tools / planning, currently spent on Clari/Forecastio + analyst time.
- **Champion:** the analyst-on-the-ground who is sick of writing post-mortems for missed forecasts and has read about Anthropic / Google / Manifold internally.
- **ICP test:** ≥200 employees, has tried internal forecasting (CRM-based, polls, or a Manifold/Metaculus pilot), missed last 2/4 quarterly forecasts by >10%, has at least one source-of-truth system Oracle can integrate with (Salesforce, Jira, GitHub, NetSuite, Looker).
- **Anti-customer:** sub-50-person companies (no information distribution to aggregate); regulated trading desks (CFTC posture, not our buyer); pure-services companies whose forecasts hinge on individual rep effort rather than aggregated information.

## Wedge / where we could enter

- **Candidate A — RevOps-led product launch dates.** Walks into the most painful fail mode (the "Q3 launch slips to Q4" drama) and matches Cowgill's Google anecdote where Prophit predicted senior-hire slippage. Resolution source: Jira/Linear ticket close. Demo-able in <5 days.
- **Candidate B — Quarterly Enterprise ARR / pipeline forecast.** Higher-value question, but contests the existing Clari/Forecastio budget directly and depends on Salesforce write access. Heavier sale.
- **Candidate C — Engineering-team milestones for AI/eng leadership.** Closest to Anthropic's pattern; Sundar Pichai answered a Gleangen question publicly [(Asterisk)](https://asteriskmag.com/issues/08/the-death-and-life-of-prediction-markets-at-google). Resolution source: GitHub PR merge / benchmark hit. Most viral on X among the buyers shopping right now.

A and C are co-led; B is the year-2 ACV expansion. Push toward C if the GTM lands inside AI-native companies and toward A if it lands in traditional B2B SaaS.

## What makes it defensible

- **(a) Primary: Connector library to enterprise systems-of-record + audited contract-template corpus.** Each new customer adds one or two source-system connectors and 5–20 contract templates that compound. After 50 customers the library is the Stripe-Atlas-of-prediction-questions; a competitor starting from zero has to re-elicit the same templates customer-by-customer.
- **(b) Secondary: Cross-platform neutrality as positioning.** We resolve markets on Manifold, Polymarket Pro, an on-prem internal instance, *or* the customer's homegrown UI. None of those vendors will become neutral; we are the only player who can.
- **(c) Year-3 endgame: A calibrated question-quality score per market (and per market-creator).** Customers learn which of their internal forecasters are systematically biased; the scoring becomes a hiring-and-promotion signal RevOps wants regardless of whether they keep using markets. This is the lock-in hook beyond the integrations.

## How it could make money

| Layer                        | Price range                  | Comparable                                                                                       |
| ---------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------ |
| **Layer 1: Question Studio** | $20–60k/yr                   | [Forecastio](https://forecastio.ai/blog/sales-forecasting-accuracy-and-analysis) (HubSpot-tier RevOps SaaS) |
| **Layer 2: Auto-resolve API**     | $5–20k/yr platform fee + per-resolution metering | [Polymarket's Dome acquisition](https://www.theblock.co/post/390546/polymarket-buys-fresh-prediction-market-api-startup-dome-marking-second-official-acquisition) (a $4.7M-seed YC unified-prediction-market API) |
| **Layer 3 (later): Question-quality benchmark + per-team calibration scores** | $50–150k/yr | [Forecastio's accuracy-tracking tier](https://forecastio.ai/blog/sales-forecasting-accuracy-and-analysis) (revenue-intelligence enterprise tier) |

Honest caveat: this can drift services-y in year 1 — every early customer will need a few high-touch question-design sessions before the template library covers their case. We need to ruthlessly productize each session into a template; if customer N needs as much hand-holding as customer 1, the bet is broken.

## What would pressure the thesis

1. **Assumption:** managers will pay for a settlement layer rather than asking their internal data team to write a SQL query and post a comment in Manifold themselves.
   - **What would pressure it:** in design-partner conversations, every champion says "I could do that with a Looker alert + Slack bot in two weeks." If this is true at three of four prospects, the wedge is too thin.
   - **Lever:** lead with the question-critic, not the connector — the AI-native tightening of the question is the part the data team won't replicate, and shifts the buy from "infrastructure I could build" to "expertise I can't hire fast enough." If the critic itself is unimpressive, kill the bet.
2. **Assumption:** internal corporate prediction markets will reach a tipping point of legitimacy in the next 18 months that is materially higher than any of the prior tipping points the literature kept hoping for.
   - **What would pressure it:** Anthropic's market gets quietly retired without a successor write-up; Manifold-for-Teams stays in pilot; no new public reference customer emerges in 12 months.
   - **Lever:** reposition as "calibrated internal forecasting infrastructure" — sell the resolvability tooling and the question-quality benchmark to teams who don't actually run markets but want the discipline. Makes us a Forecastio-adjacent product with a smaller TAM but a real one.
3. **Assumption:** the resolvability layer is genuinely AI-native enough to be a software product, not a consulting business.
   - **What would pressure it:** average customer needs >5 hours of human-in-the-loop question-design work in year 1 even after the template library has 50 entries.
   - **Lever:** narrow ICP to AI-mature companies whose data lakes are already clean, and require a customer-success-paid implementation tier so the services revenue is at least margin-positive while the template library matures. Reframe the consulting cost as on-purpose, not as failure.
4. **Assumption:** the source-system semantics that resolve markets are stable enough across customers that contract templates compound — i.e., that "shipped," "closed-won," "GA," and "ARR" mean the same thing in Acme's Jira/Salesforce/NetSuite as in the next customer's, often enough that the (a) primary moat actually accrues.
   - **What would pressure it:** in design-partner work, every customer reclassifies deals across quarters, reopens "shipped" tickets, retroactively adjusts ARR for credits/concessions, or uses bespoke ticket workflows ("done-but-pending-eng-review") that break the template's binary read. If the average new customer requires >50% template rewriting rather than reuse, the library is a Rolodex, not a moat — and Oracle is closer to a high-touch consulting business than to software.
   - **Lever:** at design-partner stage, instrument the auto-resolver against historical customer data BEFORE the live-customer cutoff and surface every disagreement (resolver says NO, customer's later state says YES). Use that delta to either (i) tighten the contract template's source-system query into something the customer's data discipline already supports, or (ii) add a thin "resolution-amendment" rule that handles the named drift class (reopens, late-reclassifications) generically. Track template reuse rate and weighted-average customizations-per-template as a leading-indicator metric. If reuse stays below 60% by customer 20, narrow ICP to companies with strict data hygiene (typically series-C+ with a data-engineering function) rather than papering over the drift with services hours.

## 2-week experiment

**Load-bearing assumption to test:** that an AI-native question-critic + auto-resolution prototype, demoed live against a prospect's *own* Jira/Salesforce data on a *real* upcoming forecast they care about, generates buying intent at the VP-RevOps / Chief-of-Staff level.

**Artifact to build (week 1):** a hosted web tool at `oracle.fyi`. Paste a draft question; the tool returns (1) a tightened binary contract, (2) the proposed source-of-truth and SQL/API query against a sample data source the prospect connects, (3) a settlement window + dispute rule, (4) a one-click "post this market to Manifold-for-Teams" or "post this market to a private Polymarket-API channel" button. Add a public scorecard at `oracle.fyi/calibration` showing the calibration of the critic against a frozen replay set of 30 historical Polymarket markets (did Oracle's auto-resolution match the actual settled outcome? what was the average question-clarity uplift?). Build with coding agents on top of Vercel + a thin Anthropic-API question-critic + the Manifold/Polymarket public APIs. ~5 days.

**Conversations (week 2):** 6–8 conversations: 3 Chiefs of Staff at Series-B/C enterprise AI startups (the Anthropic-watching cohort), 2 RevOps leads at $50–500M-ARR B2B SaaS, 2 internal-forecasting practitioners (someone running a Manifold-for-Teams pilot, someone who tried Gleangen-style markets and gave up). Open every call with the demo running on the prospect's own data — no slides.

**Specific questions / asks:**
1. Walk me to one upcoming forecast you'd use this for if it worked. Which system would resolve it?
2. Looking at the live tightened-question Oracle just produced — what would you push back on?
3. If we ship this for $40k/yr inclusive of three integrations, who signs?
4. Who already in your stack would block this — and is the blocker about features or politics?
5. Would you rather we sit on top of Manifold for Teams, or run our own embedded UI?

**Pass criteria:** ≥3 design-partner LOIs at $20–40k AND ≥1 prospect names a PO date AND scorecard reaches ≥10 inbound replies (X / cold email / forwarded by champion) AND the Anthropic-question-critic auto-resolves ≥80% of the 30-market replay correctly without manual override.

**Kill criteria:** ≤1 LOI, ≤5 inbound replies, *or* the question-critic resolves <60% of replay correctly — meaning the AI-native part of the moat isn't working.

**Vincent's effort:** ~50 hours build (Vercel + Anthropic API + Manifold/Polymarket integrations) + ~25 hours conversations + ~10 hours follow-up memo. Output: live `oracle.fyi`, public scorecard URL, conversation memo with quoted answers, go/pivot/kill recommendation.

## What we don't know yet

- Whether Anthropic's internal market is still running publicly enough that the company would talk to us as a design-partner / reference customer, or whether it has gone quiet (which would weaken the "why now" anchor).
- Whether Manifold-for-Teams' pilot pricing is competitive or open enough that customers will treat the Oracle layer as additive, vs. forcing us to build our own thin market UI.
- How aggressively Polymarket extends post-Dome into the corporate / private-market segment — there's a non-zero risk they ship a Polymarket Enterprise that bundles a thin version of resolvability themselves.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Conviction — AI-populated forecasting markets for enterprise operations]]
- [[Tally — Internal prediction markets that allocate coding-agent budget across engineering teams]]
- [[Bookmaker — Settlement-grounded routing markets that turn every CI run into a calibrated bet on which model should do the work]]
