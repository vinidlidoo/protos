---
proto_generator:
  seed: 455901942
  writer: 2
  writers_total: 2
  repo_sha: 5106d57
  generated_at: 2026-04-28T21:12:07+00:00
id: proto-bellwether
aliases:
  - Bellwether
tags:
  - proto
type: proto
status: drafted
created: 2026-04-28
origin: ""
---

# Bellwether — private on-prem eval harness for enterprise coding-agent fleets

## What is it?

**Elevator pitch.** Bellwether is an on-prem evaluation harness for enterprises that have rolled out coding agents (Claude Code, Cursor, Copilot, Codex) to hundreds or thousands of engineers. We give the platform team a private, repo-grounded scorecard that tells them which agents, prompts, and policies are quietly regressing — without sending a line of source code, ticket text, or agent trace outside their VPC.

**How it works.** A platform team installs Bellwether inside their network — a sidecar that taps the company's AI gateway (Portkey, LiteLLM, or a proxy) and a runner that re-plays a curated set of the company's own past PRs and tickets through each agent configuration on a schedule. The runner produces a private leaderboard: per-agent, per-team, per-policy quality scores on the firm's own codebase, plus diffs against last week's run. When a model upgrade lands, when a security policy changes, when a team rolls out a new prompt template — the platform team sees the regression *before* engineers file tickets, and can roll back at the gateway. Nothing leaves the customer's environment; the eval models, the traces, and the firm's code all stay inside.

## Why now (2026)

- **Coding agents are now load-bearing inside large enterprises.** Claude Code has reportedly passed Copilot in developer share, with usage at ~75% inside companies under 200 engineers ([Pragmatic Engineer, AI tooling 2026](https://newsletter.pragmaticengineer.com/p/ai-tooling-2026)). Anthropic's own 2026 Agentic Coding Trends report is the artifact a CIO will be handed at every board meeting this year ([Anthropic, 2026 Agentic Coding Trends Report](https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf)).
- **AI-generated code carries a measurable quality tax.** A study of 470 GitHub repos found AI PRs ship 1.7x as many bugs as human PRs and 75% more logic/correctness errors per 100 PRs ([Stack Overflow, Are bugs and incidents inevitable with AI coding agents?](https://stackoverflow.blog/2026/01/28/are-bugs-and-incidents-inevitable-with-ai-coding-agents/)). A separate survey reports 43% of AI-generated changes need debugging in production after passing QA ([VentureBeat, 43% of AI-generated code changes need debugging in production](https://venturebeat.com/technology/43-of-ai-generated-code-changes-need-debugging-in-production-survey-finds)).
- **Enterprise codebases break agents in ways public benchmarks hide.** SWE-Bench Pro's commercial split — proprietary repos from real partner companies — shows the best frontier models scoring under 20%, vs. much higher numbers on the public set, exposing a wide gap between public leaderboards and what works on a real firm's code ([Scale, SWE-Bench Pro paper](https://arxiv.org/pdf/2509.16941)).
- **The privacy gate is closing on third-party LLM eval SaaS.** EU AI Act high-risk obligations (technical documentation, conformity assessment, registration) bind from 2 August 2026 ([European Commission, AI Act regulatory framework](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)), and the Act now also requires training-data disclosure and provider-side risk management. Sending source code and prompts to a SaaS evaluator is exactly the kind of cross-border AI processing security and legal teams are starting to block.
- **The vendors customers already trust gave themselves the hooks but not the harness.** Anthropic opened Claude Cowork in April 2026 to customer-operated control planes for inference, identity, audit, and plugin supply chain — three extension points and five managed-preference keys that route every chat turn and tool call to a customer-controlled gateway ([systemprompt.io, Claude Cowork plugins and self-hosted enterprise deployment](https://systemprompt.io/guides/claude-cowork-plugins-enterprise)). That is a clean integration point for a third-party evaluator that runs *inside* the customer.
- **Recent incidents have made "agent quality" a board-level question.** 2025 saw an unprecedented number of incidents and was the year AI-assisted dev "entered its acceleration era" ([CodeRabbit, 2025 was the year of AI speed; 2026 will be the year of AI quality](https://www.coderabbit.ai/blog/2025-was-the-year-of-ai-speed-2026-will-be-the-year-of-ai-quality)). Whoever owns the agent fleet now has to answer "how do we know it's getting better, not worse?"

## Who else is doing this

- **Cloud LLM observability / eval SaaS** — leader: **[Braintrust](https://www.braintrust.dev/)**. Others: [LangSmith](https://www.langchain.com/langsmith), [Langfuse](https://langfuse.com/docs), [Datadog LLM Observability](https://www.datadoghq.com/product/ai/llm-observability/). Strong eval primitives, but the default deployment ships traces and prompts to their cloud — exactly what a regulated buyer is now blocking. Self-hosted tiers exist but are bolt-ons, not the product.
- **Safety / red-team eval vendors** — leader: **[Patronus AI](https://patronus.ai/)**. Others: [Lakera](https://www.lakera.ai/), [Robust Intelligence (now Cisco)](https://www.cisco.com/site/us/en/products/security/ai-defense/robust-intelligence-is-part-of-cisco/index.html). Patronus offers an on-prem option ([Patronus on AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-qhhbedrtmc4zo)) but the product is generic agent safety, not coding-fleet quality regression on a specific codebase.
- **AI gateways with built-in observability** — leader: **[Portkey](https://portkey.ai/features/ai-gateway)**. Others: [LiteLLM](https://www.litellm.ai/), [Kong AI Gateway](https://konghq.com/blog/engineering/ai-gateway-benchmark-kong-ai-gateway-portkey-litellm). They see every request, but their scoring is generic (latency, cost, guardrail hits). They are a *channel* for Bellwether, not a competitor.
- **Public coding-agent benchmarks** — leader: **[SWE-bench](https://www.swebench.com/)** and the SWE-bench family ([SWE-Bench Pro](https://labs.scale.com/leaderboard/swe_bench_pro_public)). Influential as buying signals but evaluate on public open-source repos. By design they cannot tell a bank whether *its* agent stack regressed on *its* monolith last week.
- **The agent vendors themselves** — Anthropic ships [Claude Code Enterprise dashboards](https://claude.com/product/claude-code/enterprise) (contribution metrics, OTel exports). Useful for adoption, but a single vendor's tool will never benchmark itself fairly against Cursor or Copilot, and platform teams are now multi-vendor.

**Where the opening is.** The category that is missing is "private, repo-grounded, multi-vendor agent quality." Cloud eval SaaS won't go private-by-default without cannibalising their core revenue model. Safety vendors won't pivot to coding-fleet KPIs because their buyer is the CISO, not the platform lead. Gateways won't grow a deep eval product because that breaks their "we're neutral pipes" pitch. Anthropic won't benchmark Claude against Cursor. The wedge is a small, focused product that runs entirely inside the customer, ingests their own PR history as the eval set, and ranks every agent and prompt template they're paying for.

## Why us

- **Vincent led AI model evaluations at Amazon for 2 years — direct, unfair exposure to how a hyperscaler measures AI quality, regression and risk at fleet scale.** That is the exact playbook a Fortune-500 platform team is now scrambling to build internally and would gladly buy. Most LLM-ops founders come from infra or DevTools, not from the eval side of a hyperscaler — that gap is the moat to attack first.
- **Trilingual EN/FR/JA, native cultural fluency in three of the world's largest economies.** The buyer for a privacy-first on-prem product is disproportionately European and Japanese (regulated finance, automotive, telco) — Vincent can run the same sales motion in Tokyo and Paris that a SF-bound competitor cannot.

## Customer & buyer

- **Customer:** **Head of Developer Productivity / Platform Engineering** at a 1,000–20,000-engineer firm in regulated industries (banking, insurance, healthcare, automotive, defence-adjacent telco) that has rolled out at least one coding agent org-wide.
- **Buyer:** Same role, sometimes the **CTO** or **Chief AI Officer** when budget needs sign-off. Budget line: developer productivity tooling and/or AI governance. Typical ACV: **$120k–$300k year-1**, growing with seats and number of agents evaluated.
- **Champion:** **Staff/principal engineer running the internal AI gateway**. They already see the request volume, already get paged when an agent regression breaks a team, and have no good story for their VP.
- **ICP test:** ≥1,000 engineers using at least one coding agent + multi-vendor (≥2 of {Claude Code, Cursor, Copilot, Codex}) + an internal AI gateway already in production + a regulator or internal security policy that blocks shipping source/traces to third-party SaaS.
- **Anti-customer:** Sub-200-engineer startups (no fleet, no governance need, will use Braintrust cloud); pure-cloud-native firms with no on-prem mandate (cheaper alternatives win); single-agent shops (no need for cross-vendor scoring).

## Wedge / where we could enter

- **Candidate A — "Private SWE-Bench for your monolith."** A 5-day install that takes the firm's last 12 months of merged PRs, builds a reproducible eval set, and produces a weekly scorecard ranking every agent + prompt template in use. Buyer pays for the scorecard; the regression alerts come free. Easiest to demo, most concrete artifact.
- **Candidate B — "Gateway-attached agent QA."** Sit next to Portkey/LiteLLM and score every live agent response against the firm's own PR history asynchronously. Lower install friction but harder narrative ("yet another sidecar"); revenue depends on the gateway vendor playing nice.
- **Candidate C — "Compliance evidence pack."** Frame the same product as the EU AI Act / SOC 2 evidence layer for AI coding tools. Easier sale to a CISO, but the buyer cares about audit, not quality, so the product roadmap drifts toward checkbox features.

What pushes us to one: do the first 5 buyer conversations (in front of the artifact) gravitate toward "I need a number to show my VP" (→ A), "make it invisible to my engineers" (→ B), or "I need this for the August AI Act deadline" (→ C). A is the default; B and C become real if buyers volunteer them unprompted.

## What makes it defensible

- **(a) Primary — proprietary eval set per customer.** Every customer's eval set is generated from their own PR history and grows weekly. After 6 months in production we know more about how each major coding agent performs on *their* codebase than they or any vendor does. Switching cost is the eval set itself.
- **(b) Secondary — multi-agent benchmark across the customer base.** Anonymised cross-customer rankings ("Claude Code vs Cursor vs Copilot on TypeScript-heavy monoliths in financial services, last 30 days") become a data product no single agent vendor can publish credibly. Buyers cite it; that creates inbound.
- **(c) Year-3 endgame — the private leaderboard becomes the procurement standard.** Just as enterprises don't sign a database deal without TPC numbers, they stop signing coding-agent deals without a Bellwether scorecard. Becomes a soft tax on every Anthropic / Cursor / GitHub enterprise deal in the segment.

## How it could make money

| Layer | Price range | Comparable |
|---|---|---|
| **Layer 1 — On-prem harness, per-engineer seat** | $20–$60 / engineer / month | [GitHub Copilot Business $19 / Enterprise $39 per seat / month](https://docs.github.com/en/copilot/get-started/plans), [Cursor Teams $40 / seat / month](https://cursor.com/pricing) |
| **Layer 2 — Multi-agent gateway integration, eval-volume + policy alerts** | $40k–$200k / yr | [Patronus AI Platform on AWS Marketplace (consumption-based)](https://aws.amazon.com/marketplace/pp/prodview-qhhbedrtmc4zo), [Portkey enterprise tier](https://portkey.ai/pricing) |
| **Layer 3 (later) — Cross-customer benchmark + procurement scorecards** | $80k–$250k / yr | [Datadog LLM Observability](https://www.datadoghq.com/product/ai/llm-observability/) |

**Honest caveat.** The on-prem motion is high-touch and slower than a cloud SaaS land — first 10 customers will look like services revenue dressed as licence revenue. The remedy is to keep the harness install genuinely 5-day-able and refuse customisations that don't ship as product. The trap to avoid: turning into a bespoke AI-eval consultancy for one bank.

## What would pressure the thesis

1. **Assumption: enterprises will refuse to send code/traces to third-party LLM-eval SaaS.**
   - **What would pressure it:** Major SaaS evaluators (Braintrust, LangSmith) ship credible private-cloud / customer-VPC deployments with the same UX as their hosted product, neutralising the privacy wedge.
   - **Lever:** Move the wedge from "privacy" to "repo-grounded eval set" — even a private-VPC SaaS doesn't auto-build an eval set from your PR history. Re-pitch as "agent quality you can trust" rather than "agent quality without leaking code."
2. **Assumption: platform teams will pay for a quality scorecard separate from the AI gateway.**
   - **What would pressure it:** Portkey or LiteLLM ship a real eval product (not just metrics) bundled into their gateway pricing.
   - **Lever:** Become a Portkey/LiteLLM eval module — partner rather than compete, and capture the eval value on top of their distribution.
3. **Assumption: there will continue to be ≥3 viable coding-agent vendors worth comparing.**
   - **What would pressure it:** Market consolidates to a single dominant agent (Claude Code "wins") and cross-vendor scoring becomes uninteresting.
   - **Lever:** Pivot the scorecard from cross-vendor to cross-prompt / cross-policy regression on the dominant agent. The internal "which prompt template performs best" question survives consolidation.
4. **Assumption: enterprise codebases are different enough from public benchmarks to justify a private eval set.**
   - **What would pressure it:** Public benchmarks (SWE-Bench, Pro, Multilingual) start tracking enterprise-style codebases closely enough that buyers trust them as proxies.
   - **Lever:** Lean harder on the *regression-over-time* angle (week-on-week deltas on the firm's actual recent PRs) — a leaderboard snapshot can never replace a longitudinal scorecard tied to model upgrades.

## 2-week experiment

**Load-bearing assumption to test:** A platform-engineering lead at a 1,000+-engineer regulated firm will give 30 minutes after seeing a working private scorecard built from a public-but-realistic codebase, *and* will name a budget line and a person who could buy it.

**Artifact to build (week 1):** A working v0 of Bellwether running against a public proxy for an enterprise codebase — pick a large, gnarly OSS monorepo (e.g. Apache Airflow, ClickHouse, or PostgreSQL) and:

1. Build an eval set of 100 historical merged PRs with their original CI signals.
2. Re-play each PR's task description through Claude Code, Cursor, and Copilot agents using their CLIs/APIs in headless mode.
3. Score each agent's diff vs. the merged human diff (test pass rate, semantic-diff distance, lint/secret/security checks).
4. Publish the result as a *private demo URL* (not a public leaderboard — public would force vendor PR conversations we don't want yet) showing per-agent scorecards, week-on-week deltas, and a "regression alert" view.
5. Record a 5-minute screencast walking through one regression discovered live.

The artifact must run locally on the demo laptop with no outbound calls (proves the privacy story).

**Conversations (week 2):** 8–10 named platform-engineering / dev-productivity leads at 1,000+-engineer firms, sourced via Vincent's Seattle / Amazon network, ex-AWS contacts, and 2–3 warm intros into European banks (privacy-first ICP). Each call opens with the screencast, then the live demo on Vincent's laptop.

**Specific questions / asks:**

1. "If this scorecard ran inside your VPC, against your repo, would you install it next quarter? If no, what's missing?"
2. "Who would own the budget — you, the CTO, the CISO, AI governance?"
3. "Which agents are you running today, and how do you currently know if a model upgrade made things worse?"
4. "What would you need to see to sign a $150k design-partner contract for the next 12 months?"
5. "What's the one regression you wish you'd caught last quarter?"

**Pass criteria:** ≥3 design-partner LOIs (or written commitment to a paid pilot) AND ≥1 buyer names a PO date within the quarter AND the screencast gets ≥200 thoughtful inbound signals (HN comments, replies, "send me access" emails) when posted to the platform-engineering / LLM-ops corner of the internet at the end of week 2.

**Kill criteria:** ≤1 LOI, no named PO date from any conversation, AND <50 inbound signals on the screencast → walk away. The privacy/quality gap was either not real or not painful enough to pay for.

**Vincent's effort:** ~70 hours total. ~45 on the artifact (build + screencast), ~25 on outreach + 8–10 calls + memo. Output: live demo URL, screencast, memo with quoted answers from each call, and a go / pivot / kill recommendation.

## What we don't know yet

- Whether buyers want a *managed-service* version (we run the eval set construction for them) or a *pure product* — services-trap risk is real if the answer is "managed."
- How fast Anthropic / GitHub / Cursor will ship their own private eval modules into their enterprise tiers, and whether they'd partner or compete.
- Whether a Tokyo / Paris go-to-market really pulls ahead of a SF default, or whether the 2026 buyer cycle in those geographies is too slow for a seed-stage company.
- Whether the eval models themselves (the "judge" LLMs) can run fully on-prem at acceptable quality — open-weight judges may be the bottleneck.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Anthropic, 2026 Agentic Coding Trends Report](https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf) — landscape report a CIO will be handed; useful framing for buyer conversations.
- [Pragmatic Engineer, AI tooling 2026](https://newsletter.pragmaticengineer.com/p/ai-tooling-2026) — practitioner-facing snapshot of agent adoption splits.
- [SWE-Bench Pro paper (arXiv 2509.16941)](https://arxiv.org/pdf/2509.16941) — strongest single source for the public-vs-enterprise eval gap.
- [European Commission AI Act regulatory framework](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — primary regulator timeline; the August 2026 deadline anchors the "why now."

## Related

- [[Protos/proto template]]
