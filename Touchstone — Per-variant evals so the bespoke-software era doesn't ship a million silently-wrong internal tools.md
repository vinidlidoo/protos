---
id: proto-touchstone
aliases:
  - Touchstone
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
proto_generator:
  seed: 846313158
  writer: 2
  writers_total: 3
  repo_sha: 7c0132d
  generated_at: 2026-04-30T09:03:41+00:00
---

# Touchstone — Per-variant evals so the bespoke-software era doesn't ship a million silently-wrong internal tools

> **Per-section word caps are budgets, not quotas.** Under is fine. +20% on a single section is fine if another runs short.

## What is it?

**Elevator pitch**: Touchstone sells a desktop-side "trust runtime" to the IT or platform-engineering team at companies that have started letting non-engineers fork their own internal-tool variants with coding agents. We continuously re-run a small suite of golden-input checks against each user's personalized variant — the way unit tests guard a single shared codebase — and give the platform owner one dashboard showing which of their 4,000 ops-team variants still match organizational ground truth, which silently drifted, and which need to be re-grounded against a refreshed source-of-truth spec.

**How it works**: Platform owners write a *touchstone spec* once for each shared underlying primitive (e.g., "the commission-calculation app must always agree with `payroll.commission_rules` for these 50 reference deals"). Every time a user generates or edits their personal variant — via Lovable, Retool's Agent surface, OpenAI's generative-UI runtime, or an in-house coding-agent harness — Touchstone replays the spec against the new variant in a sandbox, scores the disagreement, and either auto-blocks the publish or flags the variant for review. The eval engine itself is small enough to run inside the customer's VPC.

## What's the problem?

When every employee builds their own variant of an internal tool, the organization loses the one thing shared SaaS gave it: confidence that two people clicking the same button get the same answer. YC's *Dynamic Software Interfaces* RFS already flags this future explicitly — "users designing widely different interfaces" sharing "underlying primitives" — and asks whether vendors will "have to deliver source code rather than packaged binaries" to enable it ([YC RFS Summer 2026](https://www.ycombinator.com/rfs#dynamic-software-interfaces)). Today the "QA every variant" job has no owner: the user who forked the tool isn't an engineer, the platform team can't manually review 4,000 variants, and the underlying SaaS vendor disclaims everything past the fork. The current workaround is to forbid forking — which kills the productivity unlock.

## Why now (2026)

- **YC has explicitly RFS'd "Dynamic Software Interfaces"**, framing it as users becoming "their own forward deployed engineers" who customize an underlying primitive set rather than consuming a one-size-fits-all SaaS — and asks how the delivery stack must change to support it ([YC RFS, Summer 2026](https://www.ycombinator.com/rfs#dynamic-software-interfaces)). When YC writes the brief out loud, the wave is already cresting.
- **The same RFS batch also calls for "SaaS Challengers"** explicitly because "AI has collapsed the cost of producing software by 10–100x", inviting clones at one-tenth price and bundled AI-native replacements of legacy ERPs ([YC RFS, Summer 2026](https://www.ycombinator.com/rfs#saas-challengers)). Two of fourteen RFS bullets pointing at variant-software is convergent signal.
- **Retool has shipped agents-priced-per-hour and is shipping eval surfaces inside its app-builder** ([Retool pricing — Agents section](https://retool.com/pricing)) — the dominant internal-tools incumbent treats per-app evals as table stakes, which means the buyer category ("platform team that owns internal-tool quality") now exists in budget form.
- **Standalone AI-eval companies are scaling on their own** — Braintrust runs a metered Pro tier at $249/mo plus per-GB and per-score overage ([Braintrust pricing](https://www.braintrust.dev/pricing)), and LangSmith Observability lists Klarna, Rippling, Workday, Cisco, and Coinbase as named customers ([LangSmith Observability](https://www.langchain.com/langsmith)). Eval-as-a-product has crossed from "researcher tool" to "regulated-enterprise line item" — but every existing offering scopes itself to evaluating a *model*, not a *user-forked app variant*.
- **a16z just published the explicit framing** that users don't want recall, they want competence — and that the central design question for any post-deployment learning system is "where does compaction happen" ([Why We Need Continual Learning, a16z, 2026-04-22](https://www.a16z.news/p/why-we-need-continual-learning)). The buyer-side translation: when each variant has compressed organizational knowledge differently, you need a measurement layer that can re-derive whether the compression still maps to ground truth. That measurement layer is Touchstone.
- **The continual-learning piece also names "auditability breaks down because a continuously updating model is a moving target that can't be versioned, regression-tested, or certified once"** as one of the unsolved problems blocking parametric learning in production ([Why We Need Continual Learning](https://www.a16z.news/p/why-we-need-continual-learning)). The same moving-target problem applies to user-forked software — and is solvable today with goldens, even if it isn't for weights.

## Who else is doing this

- **Eval/observability-for-models** — main player: **[Braintrust](https://www.braintrust.dev/pricing)**. Others: [LangSmith](https://www.langchain.com/langsmith), [Patronus](https://www.patronus.ai/pricing). They evaluate prompts/agents/models against datasets, not user-forked applications against a shared organizational spec. Their unit of evaluation is "an LLM call"; ours is "a variant app's behavior on a golden workflow."
- **Internal-tool builders adding eval surfaces** — main player: **[Retool](https://retool.com/pricing)** with Agents observability/evaluations bundled into the platform. They're the natural distribution channel and the natural threat — but Retool's eval surface is scoped to agents *they ship*, not third-party variants generated outside their canvas.
- **AI app builders enabling end-user variants** — main player: **[Lovable](https://lovable.dev/)**. Cursor and the broader coding-agent stack let any employee fork business-logic apps. None of them ship a "does this fork still satisfy organizational invariants?" check; they assume the user is the only stakeholder.
- **Test-generation and traditional QA** — historically Selenium/Playwright/Cypress; in the AI era, agentic testers like Octomind and Reflect. Built for "a QA team writes tests for one shared product"; doesn't translate to "1 spec, 4,000 variants, no QA team."

**Where the opening is**: Every existing eval product owns the *model side* of the trust boundary. Every existing internal-tool platform owns the *build side*. Nobody owns "this user just forked a tool — does the new fork still satisfy what the organization actually needs from this category of tool?" The natural future owner is whoever holds the **per-variant spec catalog** — a layer that the model evaluators can't see (they don't know what a Lovable app even is) and that internal-tool incumbents can't fully claim (they only see variants built on their own canvas, not the long tail of forked-elsewhere tools that increasingly land in the same Slack channel).

## Why us

- **Two years running AI model evaluations inside Amazon** — the muscle memory for what a *useful* eval suite looks like vs. a vanity benchmark, and the scar tissue of how large orgs actually adopt regression and risk tooling. The hardest problem here isn't building a runner; it's getting platform owners to write specs they trust enough to block on. That is exactly the muscle the Amazon AI-eval years built.
- **Time-series-DB bizdev experience** — selling a horizontal infra primitive (TSDB) to skeptical platform teams maps cleanly to selling Touchstone to the same buyer.

## Customer & buyer

- **Customer**: Platform engineering or internal-tools lead at a 1k–10k-person company that has rolled out Lovable / Retool / a homegrown coding-agent harness to non-engineers and is starting to see variant proliferation.
- **Buyer**: Same role; budget line is "internal developer platform" or "AI tooling." Initial ACV $30–80k expanding to $150–300k as the variant catalog grows past ~1k apps.
- **Champion**: A burned platform engineer who already had one "Sarah's variant computed bonuses wrong for three months" incident.
- **ICP test**: ≥500 active employee-built variant apps in the last 90 days, and ≥1 named incident traceable to a forked variant disagreeing with source-of-truth data.
- **Anti-customer**: Companies that are still gatekeeping all internal tools through engineering review — no variant proliferation means no Touchstone problem.

## Wedge / where we could enter

- **Candidate A — Retool variant evals**: Plug into Retool's Agent + app-builder surfaces first, since Retool already markets evaluations and has the budget conversation open. Risk: Retool builds it themselves; we become a feature.
- **Candidate B — Lovable / coding-agent variant evals**: Sit on the publish-time hook for end-user-built apps that *aren't* on a managed platform. Greenfield, but distribution is harder because no incumbent is evangelizing the buyer.
- **Candidate C — "Spec-from-existing-flow" for one vertical**: Pick commission/compensation calculations or pricing-exception tools at one mid-market SaaS company and offer to extract goldens from their *existing* shared internal tool, then guard variants with them. Narrowest, lets us prove the spec-extraction primitive works.

Push toward C if the spec-authoring step turns out to be the load-bearing bottleneck (likely); push toward A if buyers prove willing to write specs themselves once Retool's marketing has primed them.

## What makes it defensible

- **(a) Primary — the spec catalog**: Once a customer has 200 organizational touchstones authored, switching cost is high and every new variant they ship makes the catalog more valuable. The Tessera-style move: derive the initial spec catalog from the user's *existing* shared internal tool — capture revealed-preference behavior on real production traffic and propose goldens automatically, sidestepping the "nobody wants to write specs" cold-start.
- **(b) Secondary — variant fingerprint database**: Across customers we learn which classes of variants drift in which ways, which compounds into proactive flags ("4 of 12 customers who forked the commission tool this way had a drift incident within 30 days").
- **(c) Year-3 endgame**: Become the default trust runtime that *every* bespoke-software platform (Retool, Lovable, in-house) integrates by reference, the way Datadog became the default observability layer regardless of cloud.

## How it could make money

| Layer | Price range | Comparable |
| --- | --- | --- |
| **Per-variant eval runtime (metered)** | $0.50–$2 / variant / month | [Braintrust Pro $249/mo + $1.50/1k scores](https://www.braintrust.dev/pricing) |
| **Platform seat — spec authoring + dashboard** | $30–80k / year per platform team | [Retool Business $50/builder, $15/internal user](https://retool.com/pricing) |
| **Enterprise — multi-spec catalog, on-prem runtime, RBAC (later)** | $150–400k / year | [Patronus Enterprise — on-prem + custom eval models](https://www.patronus.ai/pricing) |

**Business-model risk**: if Retool (or whichever app-builder owns the most variants) decides per-variant evals is core platform, we're a feature. Mitigation is to be cross-platform from day one and to win the long-tail of in-house coding-agent harnesses where no single incumbent has gravity.

## What would pressure the thesis

1. **Assumption**: Variant proliferation hits a scale (>500 active variants per company) where a platform owner genuinely cannot review by hand within the next 18 months at our target ICP.
   - **What would pressure it**: Surveys of Retool / Lovable customers showing the median "variants in production" is still <50, with no growth curve. Or large incumbents (Workday, ServiceNow) successfully forbidding variants entirely.
   - **Lever**: Move down-market to platforms like Notion / Glide where end-user variant counts are already large but per-variant ACV is too small to support our pricing — and shift to a usage-based, no-platform-fee tier.
2. **Assumption**: Platform teams will pay for a *third-party* trust layer rather than wait for Retool/Lovable to ship it natively.
   - **What would pressure it**: Retool's Agents-evaluations surface ([retool.com/pricing](https://retool.com/pricing)) maturing into a per-variant trust runtime within 12 months, bundled at no incremental cost.
   - **Lever**: Pivot to the cross-platform play earlier — sell to companies that have *both* Retool and Lovable and homegrown harnesses, where no incumbent's native solution is sufficient. The fragmentation is the moat.
3. **Assumption**: Goldens are the right primitive — i.e., organizations have stable enough "ground truth" inputs to write touchstones against.
   - **What would pressure it**: Customer interviews where the ground truth itself changes weekly (commission rules, pricing tiers), making goldens stale faster than they can be authored.
   - **Lever**: Shift product center of gravity from "static touchstones" to "live differential evals" — diff every variant's output against the authoritative shared tool's output on the *same live input*, no hand-authored spec needed. (This is closer to Bookmaker's settlement-grounded routing than to traditional eval suites — a nearby vault proto worth re-reading if we go this direction.)

## 2-week experiment

**Load-bearing assumption to test**: Platform owners at companies that have already deployed Lovable or Retool to non-engineers will (a) recognize the variant-trust problem when shown a working artifact and (b) pay for a third-party runtime rather than wait for the platform to ship it native.

**Artifact to build (week 1)**: A working Touchstone v0 — a CLI + dashboard that ingests a Retool app export (or a Lovable project URL), accepts a small YAML touchstone spec ("when input X, output should agree with shared spreadsheet Y on column Z"), and runs a sandboxed replay producing a per-variant pass/fail/drift score. Hosted demo with 3 forked variants of one realistic ops tool (commission calculator) showing one silently-wrong variant flagged. ~5 days solo with coding agents — the runner is mostly orchestration around a headless Retool runtime + a small judging LLM.

**Conversations (week 2)**: 10 platform-engineering / internal-tools leads at companies with named Retool or Lovable rollouts (sourced via the customer logos on Retool's site + LinkedIn search for "platform engineering manager" + "Retool" or "Lovable"). Open every call by sharing the screencast of the silently-wrong variant getting caught.

**Specific questions / asks (each answerable in 30 minutes with the demo on screen)**:
1. How many variants of internal tools are live at your company today? Growth rate?
2. Has a forked variant ever produced a wrong number that hit a real decision? What was the cleanup cost?
3. Who owns "is this variant still right?" today — and what would it take to give them this dashboard?
4. Would you pay $50k/yr for this if it covered your top-20 critical workflows? What would have to be true?
5. Would you write the touchstones yourself, or would you only adopt this if we extracted them from your existing shared tool?

**Pass criteria**: ≥3 LOIs from named platform teams committing to a paid pilot AND ≥1 pulls out a PO date within 60 days AND ≥30 inbound replies / GitHub stars on the public artifact.

**Kill criteria**: <2 of the 10 calls flag variant-trust as a problem they'd pay to solve in the next 12 months, OR ≥3 confirm they're already waiting on Retool's native solution and won't add a third-party layer.

**Vincent's effort**: ~50h total — 30h building the artifact, 20h on outreach + calls. Output: hosted artifact + a memo with quoted answers + go/pivot/kill recommendation.

## What we don't know yet

- What fraction of variants are "spec-able" — some workflows may be too creative-judgment-shaped for goldens to capture.
- Whether the right initial selling motion is bottom-up (developer-tool style, free CLI → team) or top-down (platform-team ACV from day one).
- Whether Lovable / Cursor / Replit will expose the publish-time hook we need, or whether we'll have to scrape app exports.
- What the right format is for a "touchstone spec" — YAML, executable Python, natural language judged by an LLM, or something else.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]] — different unit of analysis (the agent vs. the variant), but the eval-runtime engineering and the buyer overlap.
- [[Bookmaker — Settlement-grounded routing markets that turn every CI run into a calibrated bet on which model should do the work]] — the lever-3 fallback (live differential evals against a settling ground truth) is closer to Bookmaker's mechanic than to classical evals.
- [[Conviction — AI-populated forecasting markets for enterprise operations]] — adjacent in spirit (organizational ground truth from many distributed signals); different buyer.
