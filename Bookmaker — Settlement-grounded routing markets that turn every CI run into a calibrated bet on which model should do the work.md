---
proto_generator:
  seed: 699040402
  writer: 2
  writers_total: 2
  repo_sha: 06b2dc0
  generated_at: 2026-04-30T04:23:31+00:00
id: proto-bookmaker
aliases:
  - Bookmaker
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
---

# Bookmaker — Settlement-grounded routing markets that turn every CI run into a calibrated bet on which model should do the work

## What is it?

**Elevator pitch.** Bookmaker is the routing layer a VP of Engineering installs in front of their coding-agent fleet so that every routed task is also a logged, settled bet on which model/agent should have done it. Instead of paying a vendor to guess which model is best for your code, you get a continuously-updated, per-team scorecard backed by your own resolved outcomes — and a router that improves week-over-week without you tuning anything.

**How it works.** The buyer points their existing agent harness (Claude Code, Codex, OpenHands, internal stack — anything OpenAI-API-shaped) at our gateway instead of directly at model providers. For each incoming task, internal "bookmaker" agents — one per registered model/vendor/internal config — post a sealed quote: probability of success and quoted token cost. The gateway routes to the chosen model, runs the task, and waits for ground-truth settlement: did the PR merge, did the eval pass, did CI go green, did the human reviewer accept. Every settled task pays out reputation (and, optionally, vendor rebates) to whichever bookmaker called it correctly. The compounding asset is the per-customer resolved-bet history: a private, calibrated oracle that grows every time the team writes code, and that we sell as the routing layer on renewal.

## What's the problem?

Engineering platform teams are running 3–7 coding agents/models in parallel today across Claude, GPT, Gemini, DeepSeek, internal forks. Per the recent a16z survey of enterprise AI buyers, "they intentionally deploy two or three AI tools for the *same* use case … redundancy is policy" ([a16z](https://www.a16z.news/p/surviving-ai-price-wars-without-destroying)). The platform team is then asked: which one for which task? Today the answer is either (a) a static rule ("Opus for hard, Haiku for easy"), (b) a vendor-side router that can't see the customer's settlement signal, or (c) ad-hoc developer choice. None of these gets sharper with the team's own data, and none of them survives the next model launch — and a new frontier model is now landing roughly weekly ([Latent Space](https://www.latent.space/p/ainews-gpt-55-and-openai-codex-superapp)).

## Why now (2026)

- **Model proliferation has crossed the bandwidth a human platform team can re-evaluate.** In a single week last month OpenAI shipped GPT-5.5 (with Codex browser control, Sheets/Slides, auto-review), Anthropic shipped Opus 4.7, and DeepSeek dropped V4 Pro/Flash MIT-licensed at 1M context — Artificial Analysis is now logging multiple new model evaluations *per day* ([Artificial Analysis Changelog](https://artificialanalysis.ai/)). Platform teams cannot re-benchmark by hand at this cadence.
- **The bake-off is now the sales motion, and buyers admit it.** Per the same a16z piece, mid-market and enterprise buyers "run parallel demos, and once something shows promise, they quickly move into a proof of concept" ([a16z](https://www.a16z.news/p/surviving-ai-price-wars-without-destroying)) — i.e., comparative evaluation is the buyer's default, not a one-time procurement event. Every team is already running an informal market; we instrument it.
- **Public benchmarks have a transferability crisis.** SWE-bench Verified leaderboards are now contaminated, gameable, and scaffold-sensitive: the public board mixes harnesses from SWE-agent, OpenHands, EPAM, Atlassian, Bytedance, and dozens of ad-hoc runners ([SWE-bench Leaderboard](https://www.swebench.com/)). Your team's score on *your* repo with *your* harness is what matters, and that signal only exists locally.
- **Prediction markets just crossed institutional escape velocity, which makes "post a probability and settle later" a buyer-legible primitive.** Kalshi was valued at $22B in March 2026 ([Wikipedia](https://en.wikipedia.org/wiki/Kalshi)) and Manifold publishes a public calibration record showing average forecast within 4 percentage points of true probability ([Manifold](https://manifold.markets/about)). Boards now know what a calibrated probability is — that wasn't true in 2022.
- **Coding-agent ground-truth is uniquely cheap to harvest.** Unlike most enterprise AI workloads, coding tasks have crisp settlement signals already wired into the dev loop: CI, test pass/fail, PR merge, code-review approval. The hard problem with prediction markets has always been resolution; here it's solved by infrastructure the buyer already runs.
- **Multi-agent systems are still fragile.** Cognition's June 2025 essay argues bluntly that "running multiple agents in collaboration only results in fragile systems … decision-making ends up being too dispersed" ([Cognition — Don't Build Multi-Agents](https://www.cognition.ai/blog/dont-build-multi-agents)). A market is not a multi-agent collaboration — it is a single decision (which model) made under structured competition. That's the one shape of agent ensemble that doesn't violate the principles Cognition lays out.

## Who else is doing this

- **Model routers / classifiers** — main player: **[Not Diamond](https://www.notdiamond.ai/)** (advertises 50%+ cost savings and 10%+ accuracy gains; OpenRouter's CEO is a public reference customer). Others: the routing modes inside [OpenRouter](https://openrouter.ai/) (advertised 5M+ users, 70T monthly tokens, 60+ providers, 300+ models). These predict which model to use from prompt features alone — they cannot see your team's eventual ground-truth (PR merged? customer happy?), so the prediction never closes the loop. Bookmaker's settlement layer is the loop.
- **AI gateways with cost / observability** — main player: **[LiteLLM](https://litellm.ai/)** (240M+ Docker pulls; Netflix uses it for "Day 0 LLM access"). Others: [Portkey](https://portkey.ai), Helicone. They give you fallbacks, spend tracking, key-vaulting — undifferentiated routing logic. They will commodity-clone a router but cannot retroactively populate a settlement history they never recorded.
- **Eval / benchmark services** — main player: **[Artificial Analysis](https://artificialanalysis.ai/)** (independent provider-by-provider benchmarks across intelligence, speed, price). Others: [SWE-bench](https://www.swebench.com/) leaderboards, Vellum, Braintrust. They sell a static or quarterly snapshot. Per-team performance on *your* repo with *your* harness drifts from the public number every time someone updates a prompt — they can't follow you in.
- **Enterprise prediction markets** — players: [Manifold](https://manifold.markets/about) (public), [Metaculus](https://www.metaculus.com/) private instances. None ships an internal market scoped to engineering throughput where the resolution event is a CI run.

**Where the opening is.** Routers don't see resolution. Gateways don't see quality. Benchmarks don't see your repo. Markets don't see code. Bookmaker is the unique vendor that owns *settled* routing decisions inside the customer's own dev loop, which is the one substrate where the ground truth is both abundant and free. Each incumbent would have to abandon their core posture to ship this: a router would have to admit it can't know which model wins until after the fact; a benchmark vendor would have to give up the universal-leaderboard pretense; a gateway would have to take responsibility for outcome quality, not just plumbing.

## Why us

- **Vincent has end-to-end coding-agent fluency (currently building this very prototype as a multi-agent harness with codified critic loops) plus an Amazon-trained instinct for how a platform team frames "which tool, when" as a buying decision.** The wedge needs a founder who can stand up the market mechanism, the gateway, and the settlement plumbing solo — and walk into a VP Eng meeting and frame it in their language. The combination is rare; both halves are load-bearing.

## Customer & buyer

- **Customer:** Platform/Developer-Productivity engineer at a 200–2,000-eng software company that has standardized on coding agents and runs 3+ models concurrently.
- **Buyer:** Director or VP of Engineering / Head of Developer Productivity. Budget line: dev-tools or AI-platform. Target ACV $60–$180k year-1.
- **Champion:** The platform engineer who currently maintains the model-selection rules in a Python config and is tired of being the bottleneck on every model launch.
- **ICP test:** Team uses ≥3 models in production *and* runs CI as a settlement signal *and* has had at least one "we standardized on X, then Y came out and we re-piloted" cycle in the past 6 months.
- **Anti-customer:** Single-vendor shops (no routing decision to make), pre-CI startups (no settlement signal), regulated buyers whose primary motivation is audit/compliance (motivation kill — they should buy a different product).

## Wedge / where we could enter

- **Candidate A — PR-resolved coding-agent router.** Drop-in proxy in front of an existing harness; settlement signal is "did the PR merge within 7 days." Single integration, public ground-truth-ish (the customer's own CI). Strongest pull, narrowest scope. Likely first move.
- **Candidate B — Eval-resolved internal-tool router.** Same mechanism but settlement is the customer's existing eval suite (Braintrust, internal harness). Higher buyer pain, requires eval discipline the customer may not yet have.
- **Candidate C — Customer-feedback-resolved AI-app router.** For AI-native B2B apps where settlement is "did the user thumbs-up." Largest TAM but slowest settlement loop and noisiest signal.

What would push us toward A: design partner already runs CI on every PR and is paying for ≥2 coding-agent vendors. What would push us toward B/C: that customer doesn't materialize but a different segment does.

## What makes it defensible

- **(a) Primary — per-customer settled-bet history compounds and cannot be ported.** Every routed task is a calibration data point against *that customer's* repo, prompts, harness, and reviewers. After 6 months a competitor cannot replicate the routing oracle without re-running all those tasks; after 18 months the gap is structural. This is the same revealed-preference-from-existing-artifacts pattern that works in apparel-fit (scan what the user already kept) — here, the artifact is every PR the team already shipped.
- **(b) Secondary — vendor-side rebate flow.** Once we route enough volume, model providers will pay to have their bookmaker tuned/featured. We become a two-sided mini-marketplace where the customer's own data ranks the vendors. This is structurally hard for incumbent gateways to match because they sell on neutrality.
- **(c) Year-3 endgame — cross-customer (anonymized) routing intelligence.** With consent, aggregate "for repos that look like X, model Y wins" signals across customers — a federated benchmark that beats public boards because it's grounded in real settled outcomes, not contests.

## How it could make money

| Layer | Price range | Comparable |
| ----- | ----------- | ---------- |
| **Layer 1 — Gateway + router seat** | $60–$180k/yr per org | [LiteLLM Enterprise](https://litellm.ai/) (custom-quoted; comparable AI-gateway tier) |
| **Layer 2 — Settled-bet scorecard / consumption** | $0.001–$0.01 per settled task | [OpenRouter](https://openrouter.ai/) usage-based pricing across 60+ providers |
| **Layer 3 (later) — Vendor-side placement / rebate share** | rev-share on routed token spend | [Not Diamond](https://www.notdiamond.ai/) commercial routing (cost-savings share with customer) |

Honest caveat: the gateway layer is competing against an open-source default (LiteLLM) that is good enough for many teams. Layer-1 ARR alone won't justify the company; the bet is that the settled-history asset (Layer 2 + 3) is what locks in value, and that asset only accumulates if Layer 1 is sticky enough to keep the volume flowing.

## What would pressure the thesis

1. **Assumption:** PR-merge / CI-pass is a clean enough settlement signal to produce a calibration curve customers trust.
   - **What would pressure it:** Design partners can't reliably tag which agent did which PR (multiple agents touch the same PR, humans rewrite chunks, settlement is fuzzy). Or: PR-merge correlates with reviewer politeness more than agent quality.
   - **Lever:** Move settlement upstream to the per-tool-call eval (test pass on the agent's own diff before any human touches it). Narrows the product to teams with serious eval infra but keeps the mechanism intact.
2. **Assumption:** A market mechanism beats a learned classifier (Not Diamond, Martian) on per-customer routing accuracy after enough settled history.
   - **What would pressure it:** A simple bandit over a learned reward model matches our calibration with less plumbing, and customers prefer the simpler story.
   - **Lever:** Repurpose the settlement layer as the labeled-training data for a per-customer reward model and present the market UI as optional. The asset is the labels, not the auction.
3. **Assumption:** Vendors will eventually pay to be ranked highly on per-customer scorecards (Layer 3).
   - **What would pressure it:** Frontier vendors view rankings the way Apple views App Store reviews — they don't pay, they negotiate placement directly with big customers.
   - **Lever:** Drop Layer 3 from the financial model; keep it as a 2028+ optionality bet, not a thesis pillar.

## 2-week experiment

**Load-bearing assumption to test:** Can we produce a per-customer routing decision that, on a real repo's last 50 PRs, beats both the team's status quo (single-model default) and a public-benchmark-driven router (Not Diamond / OpenRouter auto) on a measurable metric (success rate × cost) — using only that team's own settled history?

**Artifact to build (week 1):** A public, runnable demo: `bookmaker-replay` — a CLI that takes a GitHub repo URL + the last N merged PRs, replays each PR as a coding task across 3–4 frontier models with a stock harness, scores each by "does the produced patch pass the merged-version's tests," then plots the per-model calibration vs. a market-aggregated routing decision. Hosted scorecard for one open-source repo (a real one, e.g., a popular FastAPI library) live on the public web. Built solo in 5 days using coding agents.

**Conversations (week 2):** 6–8 named Heads of Developer Productivity / Platform Engineering at companies in our ICP (200–2,000 eng, multi-model). Each conversation opens by running `bookmaker-replay` against *their* repo on a screenshare. They watch their own calibration curve render in real-time.

**Specific questions / asks:**
1. Looking at this scorecard for *your* repo, what would change in your platform's routing config tomorrow?
2. Would you let us run this continuously against your CI for 30 days, free, in exchange for the scorecard being yours to keep?
3. If after 30 days the scorecard correctly predicts which model wins per-task with ≥X% calibration, is there a budget line that pays for this on renewal?
4. Who else inside your org needs to see this scorecard — and which of them controls a budget?

**Pass criteria:** ≥4 design-partner LOIs *and* ≥1 budget-owner names a renewal price *and* `bookmaker-replay` gets ≥50 GitHub stars or ≥3 inbound from non-pitched companies.

**Kill criteria:** <2 LOIs after 8 conversations; or replay scoring shows the market-aggregated decision is statistically indistinguishable from "always pick the cheapest model that passes a smoke test"; or design partners say "interesting but I'd let LiteLLM ship this in their next release."

**Vincent's effort:** ~50 hours build (artifact + replay infra + hosted demo) + ~25 hours conversations. Output: the live `bookmaker-replay` site, a memo with quoted answers from each conversation, a go/pivot/kill recommendation.

## What we don't know yet

- How fast does per-customer routing skill saturate? If 95% of the lift comes after the first 200 settled tasks, the moat is shallow.
- Do bookmaker quotes need to be model-specific or harness-specific? The same model in different harnesses (Codex vs. Claude Code vs. OpenHands) may need separate bookmakers, which fragments the market.
- Can we get vendor rebates without becoming an OpenRouter clone with worse defaults?

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [a16z — Surviving AI Price Wars Without Destroying Your Business](https://www.a16z.news/p/surviving-ai-price-wars-without-destroying) — the buyer-side observation that enterprises run multiple AI tools for the same job by design; foundational for the wedge framing.
- [Cognition — Don't Build Multi-Agents](https://www.cognition.ai/blog/dont-build-multi-agents) — argues against multi-agent collaboration; useful for distinguishing markets (a single decision under competition) from collaboration (fragile).
- [Latent Space — GPT 5.5 and Codex Superapp](https://www.latent.space/p/ainews-gpt-55-and-openai-codex-superapp) — captures the model-launch cadence that motivates an automated routing layer.

## Related

- [[Conviction — AI-populated forecasting markets for enterprise operations]] — same prediction-market mechanism, healthcare-ops vertical; sibling bet.
- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]] — adjacent dev-platform wedge with a static-eval angle.
- [[Foreman — OSS coding-agent fleet scheduler for regulated enterprises]] — same buyer (platform/devprod) but a scheduling not-routing wedge.
