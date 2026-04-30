---
proto_generator:
  seed: 400633033
  writer: 2
  writers_total: 2
  repo_sha: 2a1d25c
  generated_at: 2026-04-28T21:44:01+00:00
id: proto-conviction
aliases:
  - Conviction
tags:
  - proto
type: proto
status: drafted
created: 2026-04-28
origin: ""
---

# Conviction — AI-populated forecasting markets for enterprise operations

## What is it?

**Elevator pitch.** Conviction is a private, internal forecasting market for a hospital system's operations team — drug-shortage exposure, OR utilization, ED boarding, staffing — populated by the hospital's own clinicians *and* by LLM agents that read the hospital's data feeds. The buyer (a VP of Operations or Pharmacy Director) gets a live, calibrated probability for "will we be short on cisplatin in 14 days" instead of a static dashboard or a consultant's PowerPoint.

**How it works.** We deploy a thin market engine into the hospital's environment and connect it to their EHR exports, GPO order history, and public feeds (FDA shortage list, BLS labor data, weather). A *question generator* — built on the same multi-source-fusion knowledge graph Vincent built at Amazon — converts those signals into well-formed, time-bounded market questions ("Inpatient census >92% on any day of week 22?"). LLM agents seed liquidity and a baseline forecast; named human participants (pharmacists, charge nurses, supply-chain leads) add private signal in exchange for a small recognition budget. The compounding asset is the resolved-question history: every closed market becomes a calibration data point that tunes the agents and ranks human forecasters, which is what we sell on renewal.

## Why now (2026)

- **Public prediction markets just crossed institutional escape velocity.** Kalshi was valued at $22B in March 2026 and its contracts now sit inside Robinhood ([Wikipedia](https://en.wikipedia.org/wiki/Kalshi)); Intercontinental Exchange invested $2B in Polymarket at an $8B valuation in October 2025 ([Wikipedia](https://en.wikipedia.org/wiki/Polymarket)). Boards now know what a prediction market *is* — that wasn't true in 2018 when prior corporate-market efforts died.
- **Regulators are clearing the channel rather than blocking it.** The CFTC issued a prediction-markets advisory and an advanced notice of proposed rulemaking in 2026, and signed a coordination MOU with the SEC in March 2026 ([CFTC press releases](https://www.cftc.gov/PressRoom/PressReleases)). Internal, play-money operational markets sit well below the regulated-event-contract line, but the rule clarity de-risks the buyer's compliance review.
- **LLM agents finally fix the liquidity problem that has plagued every prior corporate market.** A long line of internal-market experiments has been documented — Google forecasting product launches, Eli Lilly forecasting clinical-trial outcomes, Best Buy forecasting store openings ([Wikipedia](https://en.wikipedia.org/wiki/Prediction_market)) — yet none of these became standing institutional infrastructure. Our read is that thin participation was the killer: human-only markets need a busy crowd to produce a price worth looking at. Agents that read the same internal data feeds and post quotes 24/7 give every market a baseline price from day one, regardless of whether humans show up that week.
- **Headless agent-to-API workflows are becoming the assumed integration mode.** Hospitals are starting to expose FHIR endpoints and agent-callable tooling; a market engine that takes signals in via API and emits a probability via API fits the way ops teams will actually wire systems together in 2027–2030.
- **Crowd-aggregation forecasting now has a 15-year empirical track record.** The IARPA Good Judgment Project showed superforecaster crowds outperformed intelligence analysts with classified access by ~30% ([Wikipedia](https://en.wikipedia.org/wiki/Philip_E._Tetlock)); Iowa Electronic Markets beat election polls 74% of the time across five presidential cycles ([Wikipedia](https://en.wikipedia.org/wiki/Iowa_Electronic_Markets)). The methodology is no longer speculative — what's missing is a vertical-specific productization.
- **Continual-learning architectures are an open research problem, but markets sidestep it.** a16z's April 2026 piece on continual learning argues LLMs still can't compress new experience into weights ([a16z News](https://www.a16z.news/p/why-we-need-continual-learning)). A market where agents post quotes and get scored against ground-truth resolutions is a *deployment-time* learning loop — you don't need to retrain weights to keep the system improving.

## Who else is doing this

- **Public prediction-market platforms** — main player: **[Kalshi](https://en.wikipedia.org/wiki/Kalshi)**. Others: [Polymarket](https://en.wikipedia.org/wiki/Polymarket), [Manifold](https://manifold.markets/about). They run public, real-money markets; sports drives 89% of Kalshi's 2025 revenue. None ships a private vertical instance an enterprise can run on its own data.
- **Crowdsourced-forecasting / superforecaster shops** — main player: **[Metaculus](https://www.metaculus.com/)** (offers private instances and pro forecasters). Others: [Good Judgment Inc.](https://en.wikipedia.org/wiki/The_Good_Judgment_Project). These are services-shaped — staffed forecasting consulting plus a hosted question pool. They don't generate questions automatically from a customer's internal data, and they don't use agents for liquidity.
- **Healthcare ops/analytics incumbents** — main player: **[Epic](https://www.epic.com/about)** (325M+ patient records, dominant EHR). Others: Oracle Health (Cerner), ServiceNow Healthcare. They sell dashboards and rules-based forecasts inside the EHR; their cultural and pricing model rewards stable, deterministic outputs, not probabilistic ones with explicit calibration scores.
- **General enterprise AI-decision tools** — players: Palantir Foundry, Snowflake Cortex, internal Databricks builds. They give the customer a workbench to build forecasts; the customer's analyst still has to define the question, model it, and stand behind it. They don't change *who decides* — Conviction does.

**Where the opening is.** Public markets monetize entertainment volume; consulting-shaped forecasters monetize expert hours; EHR vendors monetize stability. None of them ships a turn-key, agent-populated, score-keeping decision instrument that lives inside one enterprise. The opening is the wedge between "we have dashboards" (pretends to be a decision) and "we hire McKinsey" (a $400k decision artifact with no calibration). A subscription-priced internal market that auto-asks the right questions and keeps score is a category none of these incumbents will build, because each would have to abandon the cultural posture that sells their flagship.

## Why us

- **Vincent has the rare combination of hospital/lab buyer fluency (4y at Siemens Healthineers — 2y imaging sales, 1y CRM, 1y marketing) AND hands-on multi-source data-fusion experience (3y Amazon trend-analytics knowledge graph).** The wedge requires walking into a hospital VP of Pharmacy meeting *and* shipping the question-generator that fuses FDA shortage feeds, GPO orders, and EHR exports. Most founders can do one. The combination is what makes the cold-start tractable.

## Customer & buyer

- **Customer:** Director of Pharmacy or VP of Operations at a 300–800-bed regional hospital system (the segment large enough to have an analytics function but too small to staff data scientists).
- **Buyer:** Same role; budget line is "operational analytics" or "supply-chain resilience." Typical ACV target $80–150k year-1.
- **Champion:** A clinical pharmacist or supply-chain analyst who already keeps a private spreadsheet of "things I worry about." They get attribution on accurate forecasts.
- **ICP test:** Hospital has had ≥1 documented drug-shortage-driven care substitution in the past 12 months AND uses a major EHR (Epic, Oracle Health, Meditech) AND has an analytics owner who can name the top 3 things they wish they could forecast.
- **Anti-customer:** Academic medical centers with in-house data-science teams (they'll build it themselves) and any hospital system in active EHR migration (the integration is the project, not us).

## Wedge / where we could enter

- **Candidate A — Drug-shortage exposure.** One vertical signal, public ground-truth (FDA list resolves the question), buyer feels the pain monthly. Strongest pull, narrowest scope. Likely first move.
- **Candidate B — OR / inpatient capacity.** Bigger budget, but ground-truth is internal and noisier; resolution requires EHR integration on day one.
- **Candidate C — Clinical-trial enrollment forecasting at mid-size CROs/biotechs.** Lilly already proved internal markets work here ([Wikipedia](https://en.wikipedia.org/wiki/Prediction_market)); buyer fluency is weaker but the question-generator IP transfers cleanly. Plausible second vertical.

What pushes us toward A: it's the only candidate where we can stand up a *public* baseline scorecard (forecasting national drug shortages from open data) and use that as the demo artifact before any hospital integration exists. That asymmetry — show before sell — is the proto's leverage point.

## What makes it defensible

- **(a) Primary: the resolved-question corpus.** Every market that closes is a calibration data point — agent quote vs. human quote vs. ground truth, by question type, by hospital. Year 2 we know which agent prompts and which human roles are best at which question class; competitors starting from scratch can't replicate this without running the same markets for the same duration.
- **(b) Secondary: the question-generator knowledge graph.** Hand-mapping ICD/NDC codes to FDA shortage entries to GPO contract lines is grunt work that compounds. It's the same shape of fusion problem Vincent shipped at Amazon. A copycat would need 12+ months just to reach our day-zero question quality.
- **(c) Year-3 endgame: a benchmark and a network.** A public "Conviction Index" of national operational forecasts (drug shortages, ED boarding) becomes the cited reference, the way Kalshi has become the media-distribution partner for prediction prices via its 2025 CNN and CNBC deals ([Wikipedia](https://en.wikipedia.org/wiki/Kalshi)). At that point, hospitals join partly to contribute private signal back into a shared (anonymized) cross-system forecast — a network effect on top of the corpus moat.

## How it could make money

| Layer | Price range | Comparable |
| --- | --- | --- |
| **Layer 1 — Hosted private instance** (per hospital system, annual) | $80k–$200k | [Metaculus Pro / private instances](https://www.metaculus.com/) (services-priced custom forecasts; comparable scope of bespoke deployment) |
| **Layer 2 — Cross-system anonymized index + API** (per buyer, annual) | $25k–$60k | [Good Judgment Inc.](https://en.wikipedia.org/wiki/The_Good_Judgment_Project) (custom forecasts + training; subscription-shaped) |
| **Layer 3 (later) — Outcome-linked tier for supply-chain hedging** (% of avoided substitution cost) | bespoke | [Polymarket](https://en.wikipedia.org/wiki/Polymarket) market-making economics; fee-on-volume analog |

Honest caveat: Layer 1 risks looking like a services contract — every hospital wants its own questions and every integration is bespoke. Discipline must come from the question-generator: if integration cost per hospital doesn't drop ≥30% by customer 5, this is a consulting business in product clothing.

## What would pressure the thesis

1. **Assumption: agent-seeded liquidity is enough that human forecasters stay engaged.** Past corporate markets died because participation faded.
   - **What would pressure it:** in pilot, human participation drops below 1 trade per active forecaster per week by week 8, even with attribution and recognition incentives.
   - **Lever:** lean further into agent-only forecasts (sell the agent panel as the product, demote humans to validators), or move to a higher-stakes vertical where the forecaster's own decisions are tied to the question (clinical-trial PMs forecasting their own enrollment).
2. **Assumption: hospital ops buyers will accept a probabilistic output.** Healthcare procurement culturally prefers single-number forecasts and prescriptive recommendations.
   - **What would pressure it:** ≥3 of first 5 buyer conversations explicitly ask us to "just give me the number" or balk at the calibration concept.
   - **Lever:** wrap the market output in a recommended-action layer (a thin LLM that turns the probability into "order +20% of cisplatin this week") so the buyer never sees the market unless they want to.
3. **Assumption: question-generation can be sufficiently automated that integration cost drops by customer 5.** If every hospital needs hand-built questions, unit economics break.
   - **What would pressure it:** customer 3's onboarding takes ≥80% of the engineering hours customer 1 took.
   - **Lever:** narrow the wedge harder — e.g., ship as a single-question product (drug-shortage exposure only) sold as a fixed-price SaaS; defer the multi-question platform to year 3.

## 2-week experiment

**Load-bearing assumption to test:** that a hospital ops buyer will pay for a probabilistic, agent-populated forecast over the status quo (a static dashboard or a rules-based alert), *and* that we can produce one credible enough to be worth showing them.

**Artifact to build (week 1):** a public-web Conviction Drug-Shortage Index. Using only public feeds (FDA shortage list, ASHP shortage data, recent FDA approvals/labelers, BLS labor and freight indicators), stand up a live scorecard of 30–50 open markets like "Will [drug X] still be FDA-listed as in-shortage on [date]?" Three LLM agents (different prompt strategies) post quotes daily; the page shows running Brier scores. Hosted at a public URL. Built solo with coding agents in ~5 working days: market engine + LLM agent harness + static frontend + cron job.

**Conversations (week 2):** 8–12 calls with Directors of Pharmacy or VPs of Supply Chain at 300–800-bed hospital systems, sourced from Vincent's Healthineers network and a targeted LinkedIn outreach. Every call opens with the live scorecard on a shared screen — never a deck.

**Specific questions / asks:**
1. Looking at this scorecard, which 3 questions matter to you most this quarter, and what do you currently do to answer them?
2. If we ran this *inside* your hospital with your GPO data and your pharmacist as a participant, what would have to be true for that to be worth $X/year?
3. Who else has to say yes for this to get bought, and what would they need to see?
4. Would you sign a paid 90-day pilot LOI today contingent on us hitting calibration target Y?
5. Which of your current vendors (Epic, Premier, Vizient, Wolters Kluwer) would you expect to ship this within 18 months, and what would stop them?

**Pass criteria:** ≥3 paid-pilot LOIs (≥$25k) AND ≥1 buyer names a PO date within the next quarter AND public scorecard generates ≥1 inbound from a hospital, GPO, or pharma buyer we didn't reach out to AND public Brier score beats a naive "shortage persists" baseline by ≥15%.

**Kill criteria:** zero LOIs AND fewer than 3 of 10 buyers can name a willingness-to-pay number AND multiple buyers explicitly prefer the rules-based alert they already have.

**Vincent's effort:** ~80 hours total. ~50 on artifact build (heavy use of coding agents), ~25 on conversations and outreach, ~5 on the memo. Output: live public URL to scorecard + memo with quoted buyer answers + go / pivot / kill recommendation.

## What we don't know yet

- Whether hospitals will permit even anonymized cross-system signal sharing — without it, the year-3 network effect collapses.
- Whether the "agents quote, humans add private signal" split actually keeps both populations engaged, or whether one drives out the other.
- Whether starting in clinical-trial enrollment (Lilly's old use case) would be a faster wedge — biotech buyers are more probabilistic-comfortable, and Vincent's neuroscience domain is closer to that buyer than to OR throughput.
- Pricing elasticity at the $80k–$200k band for a product hospitals have no precedent for.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Charts of the Week: 'Is Tech Cheap, Now?'](https://www.a16z.news/p/charts-of-the-week-is-tech-cheap) — a16z, April 2026. Tone-setter on quantifiable AI benefits accelerating in financial sectors; informs the operational-vs-entertainment framing.
- [Why We Need Continual Learning](https://www.a16z.news/p/why-we-need-continual-learning) — a16z, April 2026. Argues parametric continual learning is unsolved; this proto's market loop is a deployment-time score-keeping substitute.
- [Philip E. Tetlock — Wikipedia](https://en.wikipedia.org/wiki/Philip_E._Tetlock) — empirical foundation for crowd-aggregation forecasting.
- [Iowa Electronic Markets — Wikipedia](https://en.wikipedia.org/wiki/Iowa_Electronic_Markets) — long-running academic prediction market; precedent for "private/limited markets work."

## Related

- [[Round 1 protos]]
