---
id: proto-tally
aliases:
  - Tally
tags:
  - proto
type: proto
status: drafted
created: 2026-05-04
origin: ""
proto_generator:
  seed: 653513303
  writer: 1
  writers_total: 1
  repo_sha: ddb0091
  generated_at: 2026-05-04T20:46:50+00:00
---
# Tally — Internal prediction markets that allocate coding-agent budget across engineering teams

## What is it?

**Elevator pitch.** Tally is an internal prediction market that lets engineering teams *bid* — in calibrated forecasts — for next quarter's coding-agent budget. The output to leadership isn't an attribution dashboard of who already spent what; it's a forward-looking, market-priced allocation: "give Payments +$80k of Claude Code in Q3 and they'll close X tickets at 72% confidence; reallocate $30k away from Growth, where the market priced their ROI at 18%." VP Eng / CTO buys, every IC engineer participates.

**How it works.** Each engineer gets a virtual budget of forecast tokens. Once a sprint, anyone can post a contract: "Team Y will close ≥N tickets / land ≥M qualified PRs / move metric Q by ≥K if their coding-agent allotment moves from $A to $B." Teammates trade against the contract. Settlement is automatic from GitHub/Linear/Jira webhooks at sprint close; payouts use a logarithmic market scoring rule (LMSR) so traders are paid on calibration, not on volume. At quarter end, Tally collapses the market state into a one-page "redeploy this $X from low-conviction allocations into high-conviction ones" memo for the buyer. Tally sits *upstream* of CloudZero/Vantage attribution — they account for spend after it happens; Tally prices the *next* allocation before it does.

## What's the problem?

Engineering orgs went from "AI tools cost $20/seat/mo" to "$500–$2,000/eng/mo" inside one fiscal year, with adoption curves nobody forecast. Uber spent its **entire 2026 AI budget on Claude Code and Cursor in four months**, with monthly per-engineer spend of $500–$2,000 and 95% engineer adoption ([Briefs](https://www.briefs.co/news/uber-torches-entire-2026-ai-budget-on-claude-code-in-four-months/)). Today's response is per-developer caps (Apple is reported on X as setting a $300/day per-developer token budget — [@leonovco](https://x.com/i/status/2039378595211292944)), which save the bill but kill the productivity story they were buying. CFOs want a way to *redeploy* spend toward teams where the next dollar produces the most output — not freeze it. The information needed to do that — "who's actually getting leverage from agents, and where would the next $50k earn the most" — lives in the heads of the engineers themselves, and there is no mechanism today to surface it.
## Why now (2026)

- **Coding-agent budgets just crossed the threshold where allocation matters more than attribution.** CloudZero's 2026 FinOps report finds AI spend now exceeds $10M/yr at 40% of surveyed companies ([CloudZero](https://www.cloudzero.com/press-releases/20260212/)). At that scale, "give every dev the same cap" becomes a real opportunity-cost decision rather than a procurement detail.
- **Token spend is genuinely non-deterministic in a way cloud spend never was, breaking forecast-by-trend.** Vantage's CTO frames it directly: "A developer using Cursor or Claude Code for the same workload can generate a token bill that varies by an order of magnitude depending on model choice, context window depth, session length" ([Vantage](https://www.vantage.sh/blog/finops-for-ai-token-costs)). Linear extrapolation from last quarter's spend systematically misforecasts; markets handle non-deterministic forecasts well.
- **The Stratechery / O'Laughlin "compute opportunity cost" thesis lands at the team level.** Owning *demand* — i.e., deciding which of your teams gets the scarce next compute slice — is the new exercise of power within an enterprise, not just between hyperscalers ([Stratechery](https://stratechery.com/2026/mythos-muse-and-the-opportunity-cost-of-compute/)).
- **Prediction markets crossed the institutional-legitimacy threshold this year.** Combined Polymarket + Kalshi monthly volume grew from $1.2B in early 2025 to $20B+ in January 2026; ICE/NYSE made a strategic investment of up to $2B in Polymarket at an $8B post-deal valuation ([TRM](https://www.trmlabs.com/resources/blog/how-prediction-markets-scaled-to-usd-21b-in-monthly-volume-in-2026)). "Run a market on it" is a normal phrase in 2026 corporate vocabulary in a way it was not in 2024.
- **Vendors are now repricing aggressively, making the buyer's allocation problem a moving target.** Anthropic removed Claude Code from its $20 Pro signup tier and is positioning a $100/mo plan as the new home for serious users ([@GergelyOrosz on X](https://x.com/i/status/2046739299240948067)); OpenAI introduced a new $100/mo Pro tier with 5× Codex usage vs. Plus ([@OpenAI](https://x.com/i/status/2042295688323875316)). Each repricing event resets the optimal team allocation; an attribution dashboard always reports this 30 days late.

## Who else is doing this

- **AI-FinOps incumbents (cost attribution after the fact)** — main player: **[CloudZero](https://www.cloudzero.com/press-releases/20251201/)**. Others: [Vantage](https://www.vantage.sh/blog/finops-for-ai-token-costs), [Finout](https://www.finout.io/blog/claude-code-pricing-2026). They tell you who *already spent* and let you tag/allocate retroactively; CloudZero shipped a Claude Code Plugin in March 2026 ([CloudZero](https://www.cloudzero.com/press-releases/20260303/)). Their natural-language-query layer answers "what did we spend?" — they don't run forward markets and don't move the next allocation by elicited belief.
- **Engineering performance / AI-impact analytics** — main player: **[Navigara](https://therecursive.com/navigara-seed-funding-ai-developer-productivity/)** ($2.5M seed, Q1 2026). They translate GitHub/Jira/Linear activity into "Direction, Proof, Reporting" leadership signals — measurement of what *did* happen. No market, no forward allocation.
- **Inside-the-tool analytics from the vendors themselves** — main player: **[Anthropic Claude Code Analytics API](https://docs.anthropic.com/en/api/claude-code-analytics-api)**. Cursor and OpenAI ship similar dashboards. They're per-vendor and per-IC; no cross-vendor view, no team-level reallocation primitive.
- **Internal corporate prediction markets (legacy)** — main players: **[Metaculus](https://www.metaculus.com/)** (reputation-based forecasting; powers the [Bridgewater 2026 competition](https://www.bridgewater.com/bridgewater-x-metaculus-2026-competition)), Inkling, Almanis. General-purpose forecasting platforms; not tied to a budget primitive, not tied to engineering systems-of-record, no auto-settlement against GitHub/Linear/Jira.

**Where the opening is.** No one in the AI-FinOps stack is running *forward, market-priced* allocation; everyone is running backward attribution with a thicker LLM chat layer. No one in the prediction-market stack is wired into engineering systems-of-record with auto-settlement and a CFO-facing redeploy-the-budget memo. The seam is exactly the join: a market primitive whose questions are budget-allocation deltas, whose traders are the ICs who actually know whether their team is bottlenecked, and whose settlement is the same telemetry the FinOps incumbents are already reading. Tally lives one layer up from CloudZero/Vantage on the time axis (forward, not backward) and one layer down from Metaculus/Almanis on the integration axis (engineering primitives, not generic questions).

## Why us

- **Mathematical depth on calibration, scoring rules, and market design is genuinely rare among founders pitching engineering buyers.** LMSR mechanics, Brier-vs-quadratic scoring, manipulation-resistance under thin liquidity — these are the parts most cloned-from-Kalshi B2B markets get wrong, and Vincent's math/physics background plus deliberate work on prediction-market design literature is a real edge for getting the mechanism right on the first ICP.

## Customer & buyer

- **Customer:** every IC engineer in a 50-500-person engineering org — they post and trade contracts about their own and adjacent teams.
- **Buyer:** VP Engineering or CTO at a Series C-onward company with a defined coding-agent budget line ($1M-$50M/yr). Budget line: "AI tooling" or "Engineering infrastructure," typically reporting up through CFO. ACV target: $80k-$300k.
- **Champion:** the engineer or eng-ops lead who lost the most painful per-developer-cap fight last quarter — they want a different mechanism on the table next time.
- **ICP test:** spends ≥$2M/yr on coding agents AND has ≥3 distinct engineering teams competing for the budget AND has had at least one all-hands "we have to cut the AI budget" moment in the past 6 months.
- **Anti-customer:** sub-50-engineer companies (single team, no internal allocation problem); regulated industries where market-based mechanisms trip compliance friction; orgs whose CFO has explicitly framed AI tools as headcount-substitute (different mental model, different sale).

## Wedge / where we could enter

- **Candidate A — Single-team retrospective markets first.** Ship as a Slack app + GitHub/Linear webhooks: one team runs a 4-week retrospective market on its *own* sprint outcomes. No reallocation yet — just calibration. Earn the trust loop, then expand to cross-team allocation. Lowest install friction, weakest top-line story.
- **Candidate B — Quarterly redeploy-memo offering.** Ship the full cross-team market on a 90-day pilot, but the only "product" the buyer sees is a one-page memo at quarter end recommending where to move $X. Market mechanics under the hood. Strongest CFO-facing story, requires multi-team commit upfront.
- **Candidate C — Cursor/Claude-Code marketplace plugin.** Position as a sidecar to Anthropic/Cursor's existing analytics: their dashboards tell you what happened, ours tells you what would happen if you reallocate. Ride existing distribution.

What pushes us toward A vs B: A wins if early-design-partner conversations show buyers are not yet ready to redeploy (they want to *see* calibration first); B wins if a buyer who already overran their budget once will pay for the redeploy memo on a single CFO conversation. Default lean: B, because the show-don't-tell artifact maps to a CFO meeting better than to an eng-ops Slack install.

## What makes it defensible

- **(a) Primary: market-design and settlement-rule fidelity flywheel on a single primary signal.** Tally v0 settles markets against one signal — GitHub PRs-merged tagged to the bidding team — and that focus is the moat. Every team that runs a market gives Tally proprietary data on which kinds of contracts settle cleanly, which get gamed (e.g., PR-padding the night before close), and how to harden the resolution rules. Six months of multi-customer settlement data on one signal hardens the scoring rules, the eligibility criteria, and the dispute process in ways a feature-clone from CloudZero cannot replicate without running real markets at scale.
- **(b) Secondary: settlement-event normalization that survives each next signal added.** The compounding work isn't "wire eight integrations together" — it's defining a settlement-event schema clean enough that adding Linear or Jira or Anthropic Analytics in Year 2 doesn't reopen Year 1's resolution rules. Every customer onboarded sharpens the schema; clones that wire-and-pray break on the third source.
- **(c) Year-3 endgame:** Tally becomes the budget-setting layer for *all* non-deterministic spend categories inside engineering — coding agents first, then GPU pretraining runs, then experimentation/inference budgets, then potentially marketing/growth-spend on similar non-deterministic substrates. Markets generalize; attribution dashboards don't.

## How it could make money

| Layer                                     | Price range            | Comparable                                                                                                                                                                                 |
| ----------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Layer 1 — Per-engineer SaaS**           | $40–$80/IC/mo (annual) | [Cursor Teams $40/user/mo](https://cursor.com/docs/account/teams/pricing); [Claude Code Team Premium $100/seat](https://www.verdent.ai/guides/claude-code-pricing-2026)                    |
| **Layer 2 — Quarterly redeploy retainer** | $40k–$120k/quarter     | [AlphaSense Channel Checks](https://www.alpha-sense.com/resources/product-articles/channel-checks-market-insights-q3-2025/) (institutional research subscription tier, comparable cadence) |
| **Layer 3 (later) — % of repriced spend** | 1–3% of repriced spend | Negotiated outcome-share pricing — no clean public comparable in this segment yet; flagged as the speculative tier accordingly.                                                            |

Honest caveat: Layer 1 alone is a thin SaaS without the strategic-memo motion behind it; Layer 3 is the venture-scale upside but takes 18–24 months to demonstrate measurable repricing and is exposed to the same attribution wall that pushed Pacvue/Perpetua away from outcome-priced category management — *don't* lead with Layer 3.

## What would pressure the thesis

1. **Assumption:** Engineers will participate honestly in markets that affect their own team's budget, given enough mechanism design (anti-self-dealing, quadratic-cost manipulation deterrents, anonymized rendering of final memos).
   - **What would pressure it:** First two pilots show systematic ticket-inflation or cross-team collusion that the LMSR can't price out; or HR pushback that "betting on coworkers' productivity" trips a culture line.
   - **Lever:** Pivot toward AI-populated forecasting markets (calibrated agents trade against each other on the same questions) and demote human traders to dispute-resolution. Note: this collapses partway into the Conviction proto's framing — that's the structural hedge, not a separate bet.
2. **Assumption:** The FinOps incumbents (CloudZero, Vantage, Finout) won't extend their natural-language layer "forward" into market-mediated allocation themselves before Tally has a wedge.
   - **What would pressure it:** CloudZero or Vantage announces "AI Budget Markets" as a 2027 roadmap item (signals they see the seam). Their distribution into the buyer is overwhelming if they choose to.
   - **Lever:** Ship Tally as a cooperative integration with one of them rather than a competitor — sit inside their UI as the forward-allocation primitive while they keep the attribution layer. (This trades upside for a survival path.)
3. **Assumption:** Coding-agent vendor pricing volatility *continues* through 2027–2028 — i.e., the next-allocation problem stays interesting because spend keeps rebasing.
   - **What would pressure it:** Vendor pricing settles into a stable per-seat regime within 12 months (e.g., Anthropic and OpenAI both converge on $X/seat with predictable usage caps), at which point the buyer's allocation question becomes "headcount × $X," solved by a spreadsheet.
   - **Lever:** Repoint Tally at the next non-deterministic spend category (GPU/inference budgets at the application layer) where price/output non-determinism continues — but acknowledge this is a different bet with a different buyer.

## 2-week experiment

**Load-bearing assumption to test:** Will three real engineering teams at a $5M+/yr-AI-spend company actually post and trade contracts about each other's productivity, in a way that produces a CFO-readable redeploy memo at the end of a 4-week sprint, *and* will the VP Eng find the memo materially different from what their gut already said?

**Artifact to build (week 1):** A working Tally v0 — Slack-bot frontend, LMSR market engine (off-the-shelf: open-source `manifold-markets` or a thin port of an LMSR library), GitHub-PRs-merged webhook settlement (single primary signal), and a one-page "Q3 redeploy memo" generated from market state. Vincent ships solo with Claude Code in 5 working days. Output is a 5-minute screencast: real GitHub events resolving real contracts on a sandboxed dataset (an OSS repo's last sprint replayed), generating a real memo. Hosted at tally.dev (or similar), public.

**Conversations (week 2):** 8 named conversations, each starting with the screencast, then asking the buyer to walk through the memo as if it were their own org. Segments:
- 4 × VP Eng / CTO at Series C+ companies whose 2026 AI budget is on the public record as having overrun (filterable from press / X).
- 2 × Eng Ops / Platform Engineering leads at the same shape of company.
- 2 × prediction-market-mechanism designers (Polymarket / Kalshi / Metaculus alums) for hard mechanism-design pressure-testing.

**Specific questions / asks:**
1. Looking at this redeploy memo, what's the *first* objection a CFO would raise? (Looking for: anti-gaming, fairness, "this is just averaging opinions.")
2. If we ran this on your last sprint, name the contract you'd have posted.
3. Where would your finance team draw the line between "use the market's number" and "override it"?
4. What signal in your existing GitHub/Linear data would make you trust auto-settlement vs. demand a human-in-the-loop?
5. Would you pay for the memo at $80k/quarter, the SaaS at $50/IC/mo, both, or neither?

**Pass criteria:** ≥3 design-partner LOIs (specific named teams committing to a 4-week paid pilot at ≥$25k) AND ≥1 buyer surfaces a budget-cycle date for procurement AND the screencast clears ≥800 inbound signals (X replies, screencast views, eng-ops Slack inbounds).

**Kill criteria:** Fewer than 2 LOIs OR ≥2 buyers say "this is just CloudZero / Vantage in 6 months" without follow-up curiosity OR the mechanism-design reviewers flag a structural manipulation hole that Tally's design can't close without inverting the IC-trader thesis.

**Vincent's effort:** ~70 hours over 2 weeks — 40 build (Claude Code-led, weeks 1 and into week 2), 30 conversations + memo (week 2). Outputs: hosted Tally v0 + screencast + memo with quoted answers + go/pivot/kill recommendation.

## What we don't know yet

- Which side of A-vs-B-vs-C is the right wedge — depends entirely on whether the first 4 conversations validate the redeploy-memo motion or push back toward calibration-first.
- Whether GitHub PRs-merged (the committed v0 signal) holds up under early-pilot pressure or whether the *first* customer reveals a cleaner primary signal — Linear tickets-closed and Anthropic Claude Code Analytics' "tasks-completed" are the two contingency candidates, but we ship on PRs-merged unless a pilot forces the swap.
- Whether the IC-trader-vs-AI-trader split needs to be made on day 1 (HR culture risk) or can be A/B'd between two early customers.
- Whether sales motion is land via VP Eng (productivity-led) or land via CFO (cost-overrun-led) — different artifacts, different first conversation.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Conviction — AI-populated forecasting markets for enterprise operations]]
- [[Bookmaker — Settlement-grounded routing markets that turn every CI run into a calibrated bet on which model should do the work]]
- [[Foreman — OSS coding-agent fleet scheduler for regulated enterprises]]
- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]]
