---
id: proto-foreman
aliases:
  - Foreman
tags:
  - proto
type: proto
status: passed
created: 2026-04-29
origin: ""
proto_generator:
  seed: 851838007
  writer: 1
  writers_total: 3
  repo_sha: 29908bd
  generated_at: 2026-04-29T08:00:09+00:00
---

# Foreman — OSS coding-agent fleet scheduler for regulated enterprises

## What is it?

**Elevator pitch**: Foreman is an open-source control plane that platform-engineering teams install in front of their coding-agent fleet (Claude Code, Codex, Cursor) to enforce per-team budgets, repo blast-radius policy, capacity reservation, and a tamper-evident audit log of every agent action. Developers run their existing harness unchanged; finance gets a clean per-team invoice; security gets the log their CISO and external auditors will accept.

**How it works**: Foreman is a Go daemon that proxies the harness's outbound LLM traffic and tool calls. Developers point `ANTHROPIC_BASE_URL` (or the Codex/Cursor equivalent) at Foreman; their harness behaves identically. Foreman authenticates the user via SSO, looks up their team's policy bundle (budget, model whitelist, repo allowlist, runner pool), enforces it inline, signs and stores the request/response/tool-call trace in append-only storage, and forwards the call upstream. A separate scheduler component reserves capacity for declared workloads (e.g., "the migration team gets 200 parallel Codex jobs M-F 9-6 JST"). OSS core is Apache-2.0; the regulated-enterprise tier adds clustering, FISC/EU-AI-Act audit packs, and SLA support.

## What's the problem?

Stripe deployed Claude Code to 1,370 engineers and built a custom internal platform ("minions") around it that ships ~1,300 PRs per week ([Stripe customer story](https://claude.com/customers/stripe), [Lenny's Newsletter](https://www.lennysnewsletter.com/p/this-week-on-how-i-ai-how-stripe)). Most enterprises don't have Stripe's infra team and can't get the bespoke Anthropic engagement Stripe got. They face a mess: opaque per-engineer spend, no way to cap a runaway agent, no audit trail their CISO trusts, no way to reserve capacity for a critical migration, no way to prevent a junior dev's agent from rewriting a regulated repo. They mostly cope by under-rolling-out (50 seats, not 1,500), or by building a half-finished gateway internally on top of LiteLLM and abandoning it after the first incident.

## Why now (2026)

- **Fleet-scale deployments are no longer hypothetical.** Stripe runs Claude Code across 1,370 engineers; Rakuten has rolled Claude Code into engineering-wide use to "automate coding tasks... powering AI features for millions of customers" ([Rakuten 2025 AI review](https://rakuten.today/blog/rakuten-ai-in-2025-embracing-agentic-ai.html)); Anthropic has bundled Claude Code into Team and Enterprise plans, removing the procurement friction that was throttling rollouts ([DevOps.com](https://devops.com/enterprise-ai-development-gets-a-major-upgrade-claude-code-now-bundled-with-team-and-enterprise-plans/)). The buyer pool just got 10x bigger and they all hit the same governance wall.
- **EU AI Act Article 12 logging obligations bind on August 2, 2026.** Any AI system that touches "worker management" — including AI used to evaluate, monitor, or assign developer work — falls under Annex III high-risk and must automatically record events over the lifetime of the system ([Article 12 text](https://artificialintelligenceact.eu/article/12/)), with a six-month minimum retention for those logs ([Article 19 retention](https://artificialintelligenceact.eu/article/19/)) and August 2, 2026 enforcement (potentially pushed to December 2027 by the Digital Omnibus) ([Help Net Security explainer](https://www.helpnetsecurity.com/2026/04/16/eu-ai-act-logging-requirements/)). The line between "developer assistant" (low-risk) and "developer-evaluation system" (high-risk) blurs the moment a productivity dashboard ingests Claude Code telemetry — which is exactly what every enterprise is building right now ([Augment Code EU AI Act guide](https://www.augmentcode.com/guides/eu-ai-act-2026)). Tamper-evident log storage is a customer requirement we hear directly, not an Article 12 mandate.
- **Anthropic's own admin surface is thin on policy.** Claude Code for Enterprise ships SSO, SCIM, audit trails and CLAUDE.md system files, but does not document per-team budgets, capacity caps, repo-level access policy, or scheduling — buyers need a separate control plane ([Claude Code Enterprise page](https://claude.com/product/claude-code/enterprise)).
- **Generic AI gateways exist but aren't agent-aware.** LiteLLM (45k stars, used as the coping mechanism today) is "a generic LLM gateway, not specialized for coding agents" ([LiteLLM repo](https://github.com/BerriAI/litellm)); Bifrost adds clustering and budgets but is also positioned as a general-purpose gateway, not a coding-agent control plane ([Bifrost overview](https://www.getmaxim.ai/bifrost)). Neither models the unit of work that actually matters here: a coding session that runs for hours, spawns sub-agents, edits files, triggers CI, and bills 50k-200k tokens per turn ([Maxim cost-management writeup](https://www.getmaxim.ai/articles/best-ai-gateway-for-claude-code-cost-management/)).
- **Japan's FISC 13th edition (March 2025) tightened external-IT governance for financial institutions**, with explicit emphasis on third-party monitoring and oversight of cloud-delivered services ([Thales FISC brief](https://cpl.thalesgroup.com/compliance/apac/fisc-security-guidelines-japan-financial-institutions)). MUFG is moving aggressively into agentic AI ([Computer Weekly on MUFG](https://www.computerweekly.com/news/366634350/How-Japanese-banking-giant-MUFG-is-using-AI)); the gap between "we want Claude Code" and "compliance will let us deploy Claude Code" is exactly the wedge a Japan-fluent vendor can close.

## Who else is doing this

- **Generic LLM gateways** — main player: **[LiteLLM](https://github.com/BerriAI/litellm)** (45k stars, OSS, used as a stopgap by most platform teams). Others: **[Bifrost](https://github.com/maximhq/bifrost)** (Apache-2.0, Go, faster, adds clustering and hierarchical budgets in OSS). These are the right architectural pattern (proxy + governance) but model "an LLM call," not "an agent session" — they have no concept of repo allowlist, runner-pool reservation, or PR-blast-radius policy. A platform team using LiteLLM for Claude Code today still has to build the agent-specific layer themselves.
- **Enterprise agent platforms** — main player: **[Ona](https://ona.com/stories/enterprise-agent-problem)** (formerly Gitpod, pivoted to "platform layer for AI coding agents"). Others: enterprise wrappers from Cursor, Cognition. These compete on **runtime / cloud-dev-environment** (sandboxed cloud machines that agents work inside), not on **policy + scheduling**. Strong product, but they want you to migrate your dev environment to them; Foreman wants you to keep your dev environment and just install a daemon. Different shape.
- **Anthropic / OpenAI first-party admin** — Anthropic ships [Claude Code for Enterprise](https://claude.com/product/claude-code/enterprise) with SSO/SCIM/audit/OTel and central CLAUDE.md, but does not address fleet scheduling, capacity reservation, multi-vendor routing, or cross-vendor unified policy. Will keep adding admin features but will never solve "I want to use Claude Code AND Codex AND Cursor under one policy."
- **Agent infra runtimes** — **[Anyscale](https://www.anyscale.com/blog/announcing-anyscale-agent-skills-ray)** (Ray-based, GA'd Agent Skills April 2026 on Claude Code and Cursor), Modal, Beam. These are the runner-pool layer Foreman *schedules into*, not competitors — natural integrations.
- **In-house builds** — Stripe's "minions," Ramp's background agent, Microsoft 1ES. Custom-built, not productized. Validates the need; also validates that it takes a Stripe-class infra team to do it well, which is exactly why a productized OSS version has a market.

**Where the opening is**: The control-plane category has split along two axes — **generic gateway** (LiteLLM, Bifrost) and **agent runtime** (Ona, Cursor for Teams). Nobody owns the **agent-aware policy + scheduling** middle, where the unit of work is a multi-hour coding session against specific repos with a specific blast radius and a specific budget envelope. Anthropic won't build it because they only care about Claude. LiteLLM won't build it because they're committed to "generic." Ona won't build it because they want to own the runtime, not be a thin policy layer above someone else's runtime. Foreman is the OSS-first, runtime-agnostic, harness-agnostic policy + scheduler that fits between them — and the regulated-enterprise tier (FISC, EU AI Act audit packs, on-prem deployment) is the monetizable wedge that no incumbent will chase first because it's slow, services-heavy work in markets they don't speak.

## Why us

- **Vincent's Japan + EU regulated-enterprise reach is asymmetric.** Native-level JP/FR/EN, ten years on the ground in Japan, four in France. Ona is in San Francisco; LiteLLM and Bifrost are global-default-English; Anthropic's enterprise GTM in Japan is nascent. A founder who can sit in a Marunouchi conference room and walk a CISO through FISC compliance in Japanese is a genuine moat for the regulated wedge — and the OSS core gets distributed for free worldwide on GitHub, so the global TAM remains in play.
- **Amazon internal-product-consulting + 50-person team management muscle is the right shape for selling to platform-engineering orgs.** Foreman's buyer is the platform team — they think in terms of fleet, queue, capacity, SLO. That's a procurement motion Vincent has run before; it's not the same skill as selling to a CTO or a line-of-business buyer.

## Customer & buyer

- **Customer**: Platform Engineering / Developer Productivity team at a 500-5,000-engineer regulated enterprise (bank, insurer, healthcare, regulated industrial, government prime). The platform engineer is the daily user.
- **Buyer**: Head of Platform Engineering or VP Engineering. Budget line: developer-tools / infra / R&D efficiency. Typical ACV $80k-$300k for managed/audited tier; OSS is free.
- **Champion**: A senior platform engineer who has been asked by their CISO "where is the audit log for what Claude wrote last week?" and currently has no answer.
- **ICP test**: ≥300 developers using a coding agent in production AND a regulator on the buyer's neck (FISC, EU AI Act, FFIEC, HIPAA, FedRAMP) AND existing internal use of LiteLLM or a hand-rolled gateway that the team admits is a stopgap.
- **Anti-customer**: <100-developer startups (free OSS is enough); SF-bay tech companies with the in-house chops and risk appetite to build their own (Stripe is not the buyer, Stripe is the case study); pure managed-cloud shops that won't run a daemon.

## Wedge / where we could enter

- **Candidate A — Japan regulated banking, FISC-bound**: 2-3 megabank / large regional bank pilots; the painkiller is "we cannot deploy Claude Code at all without an audit-log + policy story our compliance team will sign." Slow sales cycle (6-9 months), high ACV, deep moat once in.
- **Candidate B — EU mid-size enterprise sweating the August 2026 AI Act deadline**: French/German insurers, banks, energy utilities. The painkiller is "Article 12 logging is binding in 90 days and our coding agents currently produce logs no auditor will accept." Faster cycle (3-6 months), regulatory-clock urgency.
- **Candidate C — OSS-first land-and-expand**: Ship a great open-source core, get adopted by 1,000+ platform-eng teams globally, monetize the 5% who hit a regulator. Slowest revenue ramp, biggest long-term distribution.

Probably run A and C in parallel: the OSS release is what makes Vincent credible enough to walk into a Tokyo bank meeting. C without A is a no-revenue charity; A without C means you're a consulting shop. What would push us toward A first: any one Japanese bank or insurer signing a paid pilot LOI in the 2-week experiment.

## What makes it defensible

- **(a) Primary — distribution moat via OSS adoption.** Foreman OSS becomes the default policy layer in front of Claude Code / Codex at platform-engineering teams worldwide; every install is a free demand-gen funnel for the regulated-enterprise paid tier. Compounds with stars, integrations, and the fact that pulling Foreman out is harder the longer you've been logging through it (your audit history lives there). LiteLLM's 45k-star OSS distribution is the proof this moat exists in this category.
- **(b) Secondary — regulatory-pack moat.** A paid FISC audit pack, EU AI Act Article 12 evidence pack, FFIEC pack, etc. is slow content work that a US-default vendor won't do in year one. Compounds because each new pack opens a new vertical and reuses the same engine.
- **(c) Year-3 endgame**: become the canonical "agent ledger" — the tamper-evident, cross-vendor record of every AI agent action in the enterprise — that regulators and external auditors ask for by name. Once auditors expect to see Foreman logs in a SOC 2 / FISC / AI Act review, the switching cost is structural, not technical.

## How it could make money

| Layer                                  | Price range            | Comparable                                                                                                          |
| -------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **OSS core**                           | $0                     | [LiteLLM OSS](https://github.com/BerriAI/litellm), [Bifrost OSS](https://github.com/maximhq/bifrost)                |
| **Managed / hosted (mid-market)**      | $30-$80 / dev / mo     | [Anthropic Claude Enterprise — custom, ~$5k-$15k+/mo for 100+ users per third-party estimates](https://vantagepoint.io/blog/sf/anthropic/enterprise-ai-tiers-explained) |
| **Regulated-enterprise tier (later)** | $80k-$300k / yr / org | [Bifrost Enterprise (custom, on-prem, audit)](https://www.getmaxim.ai/bifrost/pricing)                              |

Honest caveat: the OSS-distribution + paid-enterprise-tier model has a known commercial-OSS trap — the OSS users are not the buyers, and converting <2% of them is normal. The regulated wedge has to *actually* ship paid revenue inside 18 months or the math doesn't work; if it doesn't, this becomes a services-heavy compliance consultancy with a free-software side project, which is a fine business but a different one.

## What would pressure the thesis

1. **Assumption**: Anthropic and OpenAI will not ship a sufficient native admin/policy/scheduling layer fast enough to remove the gap.
   - **What would pressure it**: Anthropic ships per-team budgets, repo-level access policy, capacity reservation, and tamper-evident audit logs in Claude Code Enterprise within 12 months — and OpenAI ships the equivalent for Codex. Single-vendor enterprises would be largely served.
   - **Lever**: lean harder into **multi-vendor / cross-vendor** policy as the wedge — even if Anthropic solves it for Claude, an enterprise with Claude AND Codex AND Cursor still has no unified policy plane. Reposition the regulated tier around cross-vendor evidence.
2. **Assumption**: Regulators (EU AI Act, FISC, FFIEC) actually enforce strict logging/governance on AI-assisted developer tooling, not just on user-facing AI products.
   - **What would pressure it**: The Digital Omnibus delays Article 12 to December 2027 ([Help Net Security](https://www.helpnetsecurity.com/2026/04/16/eu-ai-act-logging-requirements/)); regulators in Japan/US treat coding assistants as out-of-scope.
   - **Lever**: shift the urgency narrative from "regulator is coming" to "your CISO is coming" — internal security/audit teams are pulling the same thread independently of regulators.
3. **Assumption**: An OSS-first distribution play can grab developer-mindshare against well-funded gateway incumbents (LiteLLM has 45k stars, two years of head start, and a similar pivot to "agent gateway" is one PR away).
   - **What would pressure it**: LiteLLM or Bifrost adds first-class "coding-agent policy" features and ships them aggressively; we lose the "agent-aware" wedge.
   - **Lever**: collapse to the regulated-enterprise wedge only (Japan-FISC and EU-AI-Act), accept being a 6-12 person profitable services-heavy company, drop the OSS distribution ambition.

## 2-week experiment

**Load-bearing assumption to test**: A platform-engineering team at a regulated enterprise, *today*, will accept a daemon-in-front-of-Claude-Code architecture as the right shape — and will find at least one of {per-team budgets, repo-allowlist policy, tamper-evident logs} acutely painful enough to pilot a paid tier within 6 months.

**Artifact to build (week 1)**: A working v0 of Foreman OSS. Public GitHub repo (Apache-2.0). Single Go binary; runs as `foreman serve`. Implements: (a) drop-in `ANTHROPIC_BASE_URL` proxy for Claude Code; (b) per-user / per-team token budget enforcement with hard cap; (c) repo allowlist policy (matches the cwd of the calling Claude Code session against a YAML allowlist; rejects with a useful error); (d) append-only NDJSON log of every request, response, and tool-call with hash-chained entries. Plus a 4-minute screencast showing all four behaviors against a real Claude Code session, and a one-page architecture diagram. Vincent solo + Claude Code, ~5 working days.

**Conversations (week 2)**: 10 named platform-engineering or developer-productivity leads — 4 at Japanese regulated enterprises (target: 1 megabank, 1 insurer, 1 large industrial, 1 internet-native like Rakuten or DeNA), 4 at EU regulated enterprises (target: 2 banks, 1 insurer, 1 government prime), 2 at US regulated enterprises (1 bank, 1 healthcare). Each conversation opens with the screencast and the live `foreman serve` binary; ends with explicit asks below.

**Specific questions / asks**:
1. Watching this 4-minute demo, which of the four behaviors (budget, repo allowlist, audit log, drop-in proxy) is most painful for you *right now*?
2. Is the daemon-in-front-of-the-harness shape a non-starter for any reason (security model, dev-laptop performance, network shape)?
3. What does your CISO/audit team need to see in a log entry for it to count as "evidence" in a FISC / AI-Act / FFIEC review?
4. If we shipped this OSS today and a managed/audited tier in 6 months, would you commit to a paid pilot at $X? What's X?
5. Who else inside your org needs to see this before you can say yes?

**Pass criteria**: ≥3 platform-engineering leads (across ≥2 regions, ≥2 of them in regulated industries) commit to a 90-day paid pilot at ≥$15k each AND ≥1 of them names a budget code AND artifact gets ≥200 GitHub stars within the experiment window.

**Kill criteria**: <2 buyers express any willingness to pay; OR every buyer says "Anthropic / our internal LiteLLM is good enough"; OR <50 stars in 2 weeks despite a Hacker News + Latent Space launch (signal: the OSS distribution thesis is broken).

**Vincent's effort**: ~80 hours total. ~50 hours building the OSS artifact and screencast (week 1), ~30 hours on conversations and write-up (week 2). Output: public GitHub repo, screencast (YouTube/Loom unlisted then public), interview memo with quoted answers, go / pivot / kill recommendation.

## What we don't know yet

- Whether the daemon proxy model survives Anthropic / OpenAI tightening their client-side TLS pinning or moving toward signed binaries that refuse non-Anthropic endpoints.
- Whether the Japanese regulated-enterprise sales motion can actually be run by a solo founder in year one, or whether it requires hiring a Tokyo-based enterprise AE on day one (very different cost structure).
- Whether the EU Digital Omnibus will or won't delay Article 12 — the Aug 2026 deadline is the urgency engine for the EU wedge.
- Whether Anthropic would view Foreman as competitive (and throttle the API) or as channel-friendly (and partner). Worth a direct conversation early.

## Vincent's Feedback

- Passed 2026-04-29 after walk-through.
- I don't get really excited about building a business that relies on regulations as the primary engine for demand. While I'm not opposed to compliance-related businesses, I find it hard to get excited by a business running on compliance to regulations that I feel is not delivering meaningful value to actual customers. This would be a motivation problem for me.
- Governance, access controls, and security-based businesses are boring. This may be a feature more than a bug for a lot of people, but I don't think I'm the person to drive such a business.
- The motivation critique above is also a structural critique of the proto. Three of the five "why now" bullets are regulation (EU AI Act Article 12, FISC, "your CISO is coming"). Wedges A and B are explicitly compliance-anchored, and Candidate C's conversion-to-paid story explicitly depends on "monetize the 5% who hit a regulator." The "why us" leans on Japan/EU regulated-enterprise reach. So this *is* a regulation-driven proto, not just one that happens to mention regulation.
- The non-compliance reframe — cost and capacity control for fleet-scale agent deployments, FinOps + VP Eng buyer instead of CISO — is a real product but not mine. It strips the "why us" advantage (Japan/EU regulated reach stops being asymmetric for a FinOps-flavored product) and puts the company in direct competition with LiteLLM's larger distribution.
- Verdict: the regulation-anchored version is a real business but fails my motivation test; the non-regulation version is a real business but isn't mine. Pass.

## References

- [Stripe customer story for Claude Code](https://claude.com/customers/stripe) — the canonical fleet-deployment proof point (1,370 engineers).
- [Lenny's Newsletter on Stripe's "minions"](https://www.lennysnewsletter.com/p/this-week-on-how-i-ai-how-stripe) — concrete description of how Stripe productionized Claude Code at scale.
- [Ona's "enterprise agent problem"](https://ona.com/stories/enterprise-agent-problem) — best articulation of the gap from a competitor's POV.
- [Maxim AI on Claude Code cost management with a gateway](https://www.getmaxim.ai/articles/best-ai-gateway-for-claude-code-cost-management/) — concrete enterprise pain points and gateway-side answers.
- [EU AI Act Article 12 text](https://artificialintelligenceact.eu/article/12/) — the legal anchor for the audit/logging wedge.
- [Help Net Security — what the EU AI Act requires for AI agent logging](https://www.helpnetsecurity.com/2026/04/16/eu-ai-act-logging-requirements/) — accessible summary of the August 2026 enforcement clock.
- [Augment Code — EU AI Act and AI-Generated Code](https://www.augmentcode.com/guides/eu-ai-act-2026) — clarifies when developer-AI tooling crosses into Annex III high-risk.
- [Latent Space — Harness Engineering with Ryan Lopopolo](https://www.latent.space/p/harness-eng) — kit article; useful framing of the "human shifts to system design" trend that makes Foreman's buyer (the platform engineer) the right ICP.

## Related

- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]] — adjacent buyer (platform engineering at regulated enterprise), different layer (eval, not policy/scheduling). Likely friendly integration, possibly bundled.
- [[Whisper — ZK attestation layer for agent-to-API calls so agents prove eligibility without leaking PII]] — complementary at the agent-to-3rd-party-API layer; Foreman is agent-to-LLM/runner.
- [[Veritrace — Cryptographically-attested eval logs that turn enterprise AI compliance from a PDF into a proof]] — same regulator-driven thesis, different artifact (eval logs vs. action logs).
