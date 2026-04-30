---
proto_generator:
  seed: 832229232
  writer: 1
  writers_total: 1
  repo_sha: 06b2dc0
  generated_at: 2026-04-30T02:48:20+00:00
id: proto-genba
aliases:
  - Genba
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
---
# Genba — Productized agent-fleet enablement program for Japanese engineering teams

## What is it?

**Elevator pitch**: A 12-week installed program that turns a Japanese mid-market enterprise's engineering team (15–60 engineers) into a working coding-agent fleet — Japanese-language curriculum, harness templates pre-tuned for keiretsu code review and quality-gate culture, embedded in-language coaching, and a measurable post-program output gain. The buyer (an engineering 部長 or DX 執行役員) gets engineers who actually use Claude Code / Cursor in anger, plus a left-behind Agent Lead inside the team who runs it after we leave. Renewable per-cohort, not consulting hours.

**How it works**: We bring the team through three phases — (1) install and configure agent harnesses in their actual repos, with team-specific `CLAUDE.md` files and slash commands matched to their existing review/QA rituals; (2) run weekly Japanese-language working sessions where engineers ship real PRs with the agents under coach observation, with feedback in keigo and references to internal naming conventions; (3) certify a designated Agent Lead and hand off a playbook + recurring office-hours subscription. The compound is a library of harness templates per Japanese industry vertical (manufacturing, finance, telecoms) — each new cohort adds patterns that make the next sale faster and the curriculum sharper.

## What's the problem?

A Japanese engineering org head sees competitors moving on AI but their own team is stuck. English-first agent tooling lands awkwardly: docs are English-only, the agents respond in stilted Japanese when prompted in Japanese, and the cultural defaults (verbose explanation, deference, ringi-style approval) don't match how Japanese engineers want to work. They've bought Cursor or Copilot seats and seat utilization is low. Internal champions burn out trying to evangelize. Big consultancies pitch ¥100M+ DX projects that never reach the engineer who actually has to type the prompt. The 部長 needs the team to *be* better at agent management within months, not a 2-year transformation deck.

## Why now (2026)

- **Anthropic just made NEC its first Japan-based global partner, deploying Claude across ~30,000 NEC Group employees and explicitly framing it as building "one of Japan's largest AI-native engineering teams"** ([Anthropic NEC announcement](https://anthropic.com/news/anthropic-nec)). When the lighthouse account in your geography stands up an internal Center of Excellence, every other Japanese enterprise board asks "what's our version" the next quarter — and most don't have an internal CoE to mimic.
- **Japan is the world's #10 developer geography on GitHub with ~3.5M developers and 23% YoY growth, but the platform's own report ties this to government's "light-touch AI regulation" rather than to coding-agent fluency** ([GitHub Octoverse 2024](https://github.blog/news-insights/octoverse/octoverse-2024/)). The headcount and growth are there; the workflow upgrade hasn't happened, and Octoverse doesn't report Japan among the top Copilot-adoption geographies.
- **Coding-agent products are aggressively English-first.** Anthropic's Claude Code documentation is hosted at `/en/` URLs with no other-language equivalents listed in the official docs index ([Claude Code overview](https://code.claude.com/docs/en/overview)). For a mid-market Japanese engineering team where junior engineers have intermediate-at-best English, this is a real adoption tax — not insurmountable, but exactly the gap a localized program closes.
- **Japanese SaaS install bases are structurally lighter — ~35 apps per company vs. ~93 global average, with only 34% of surveyed Japanese companies using any SaaS at all** ([Nihonium SaaS adoption Japan](https://nihonium.io/saas-adoption-in-japan/)). The opening: less "rip and replace 200 SaaS workflows" and more "wrap the legacy + bespoke stack with agents that read the team's own code and runbooks." The agent-fleet pattern fits this stack better than horizontal SaaS does.
- **Per-seat AI tooling is cheap relative to enablement spend.** Cursor Teams at $40/user/mo ([Cursor pricing](https://www.cursor.com/pricing)) and Copilot Business at $19/seat/mo ([GitHub Copilot plans](https://docs.github.com/en/copilot/about-github-copilot/plans-for-github-copilot)) put tooling cost at <¥10,000/engineer/month. The bottleneck is usage skill, not license fees — exactly the FinOps inversion that justifies a multiple of license spend on enablement.

## Who else is doing this

- **Japan-domestic consultancies and SIs (NRI, NTT Data, Accenture Japan, Abeam)** — main player: **[NRI](https://www.nri.com/en)**. Others: [NTT Data](https://www.nttdata.com/global/en/), [Accenture Japan](https://www.accenture.com/jp-en). They sell large DX engagements (¥100M+, 12–36 months) staffed with consultants — slide-decks, architecture diagrams, occasional implementation. Their staffing model can't profitably ship a 12-week working-with-engineers program at a price the mid-market can swallow, and their reflex is to sell the *executive*, not embed with the engineering team. They're the natural channel partner for Genba once we have proof, not the competitor.
- **Anthropic / Cognition / Cursor direct enablement** — main player: **[Anthropic](https://anthropic.com/news/anthropic-nec)** (via the NEC partnership and Forward-Deployed Engineer model). Cognition's Devin starts at $20/mo with enterprise contracts ([Devin 2.0](https://www.cognition.ai/blog/devin-2)). Vendor-led enablement is necessarily product-evangelism; their FDE bench is small and reserved for top-tier accounts (NEC, MUFG-tier). The mid-market — a ¥50–500B revenue manufacturer with a 30-engineer team — is below the FDE allocation cutoff but still wants enablement, in Japanese, that doesn't lock them to one vendor.
- **English-language cohort training (Maven, Reforge, Pluralsight)** — main player: **[Maven](https://maven.com/about)** for cohort-based courses; Reforge and Pluralsight for self-paced. These exist, are good, and are entirely in English. A Japanese engineering manager cannot enroll 30 engineers in a Maven cohort and expect comprehension or transfer to their actual repos. The product gap is "in language, in their codebase, with their review culture."
- **In-house champions and internal hackathons** — every large Japanese tech org has one or two engineers who already use Claude Code well and are trying to evangelize. They are the heroes the buyer hopes will scale, and they don't. They don't have the time, the materials, or the authority to install harness conventions across the team. They're our most valuable internal sponsors, not competitors.

**Where the opening is**: Japan-specific, engineering-team-altitude, productized enablement that ships measurable agent-usage gains in a quarter. Big consultancies won't do it (wrong unit economics, wrong audience). Vendor FDEs can't reach the mid-market at scale. English cohort schools don't translate. The opening lasts roughly the 18–36 months it takes for either (a) NRI/NTT Data to hire and train a thousand FDE-equivalents, or (b) the agent vendors to staff Japan FDE benches deep enough to serve the mid-market — both of which are slower than pulling a partner-channel ladder up behind us.

## Why us

- **Trilingual EN/FR/JA + 10 years lived in Japan + INSEAD MBA**: the rare profile that can credibly walk into a Japanese 部長's office in keigo, then translate the latest Anthropic FDE pattern from English with no semantic loss, then sell upstream into procurement on Western enterprise-buying logic. This is not a "we'll hire a Japan partner" story; it's the founder.
- **Amazon trend-analytics knowledge graph experience**: building per-cohort harness templates that wrap heterogeneous internal data sources (legacy DB, Confluence, internal wiki, code) into agent-ingestible context is exactly the multi-source data-fusion shape — directly transferable to the harness-installation phase of the program.

## Customer & buyer

- **Customer**: Engineering teams of 15–60 engineers inside Japanese enterprises with ¥50–500B revenue (mid-market — not Sony/MUFG tier, not 5-person startup). Manufacturing, financial services, telecoms, insurance.
- **Buyer**: 部長 of engineering, DX 執行役員, or CTO. Budget line: existing DX/HR-development line item, often ¥30–100M annual training/enablement bucket per business unit.
- **Champion**: The internal "AI-curious" engineer or tech lead who has tried Claude Code on weekends and is frustrated their team isn't following — usually an EM or staff engineer. They make the introduction.
- **ICP test**: ≥1 Cursor or Copilot site license already purchased, <30% measured weekly active usage, and an internal champion who can name 3 specific repos where agent fluency would unblock shipping.
- **Anti-customer**: <15-engineer teams (program economics break), pure-IT-services firms (their devs are billed-out, no slack for upskilling), or any org where the buyer is the CCO/CISO (governance-engine kill — wrong motivation).

## Wedge / where we could enter

- **Candidate A — Single-cohort pilot for one mid-sized Japanese manufacturer's R&D software team.** Discounted price (¥8M for 12 weeks), 20 engineers, in-person Tokyo / Nagoya / Osaka. Pushes us here if a champion in our network already has buyer alignment and we want a fast first reference logo.
- **Candidate B — "Agent Lead Bootcamp" 4-week sub-program.** Train designated Agent Leads from 5 different companies in one cohort (¥1.5M/seat). Pushes us here if buyer signal is strong but they want to send one person before committing the team — common Japanese procurement pattern.
- **Candidate C — Vendor-channel partnership with Anthropic Japan or Cursor Japan** as the certified Japanese-language enablement partner. Pushes us here if we land an early conversation with their Japan GTM and they want a partner network beyond the FDE bench. Highest-leverage but lowest control over timing.

Default: lead with **Candidate A**, run **Candidate B** as a parallel low-friction lead-generator, position **Candidate C** as a 12-month aspiration once we have 3 logos.

## What makes it defensible

- **(a) Primary — vertical harness template library.** Each cohort produces a Japanese-industry-specific harness pattern (e.g., automotive embedded review-culture, finance regulatory-comment style, telecoms operations-runbook agents). Templates are private IP, transfer between buyers, and make each subsequent sale shorter to deliver — classic services-to-product flywheel where IP compounds with engagements.
- **(b) Secondary — Japanese-language curriculum + community of certified Agent Leads.** A network effect at the alumni layer: certified Agent Leads from cohort 1 introduce cohort 2 buyers, the community Slack becomes a paid recurring revenue stream and a recruiting channel for our coaches.
- **(c) Year-3 endgame**: Become *the* Japanese-language enablement layer that sits between English-first agent vendors (Anthropic, Cursor, Cognition) and Japanese mid-market buyers — channel partner for vendors, training default for SI partners. Plausibly acquired by a vendor wanting Japan distribution, or an SI wanting product-shaped IP.

## How it could make money

| Layer                                    | Price range                    | Comparable                                                                                                                       |
| ---------------------------------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| **Layer 1 — Cohort program (12 weeks)**  | ¥10–20M per cohort (~$70–140K) | [Maven cohort courses](https://maven.com/about) (B2C analog at $1–5K/seat, ours is B2B closed-team pricing)                      |
| **Layer 2 — Agent Lead Bootcamp (4 wk)** | ¥1.2–2M per seat (~$8–14K)     | [Cursor Teams](https://www.cursor.com/pricing) at $40/user/mo as the underlying-tool baseline; our pricing reflects skill, not license |
| **Layer 3 (later) — Recurring office-hours + community** | ¥30–80K/engineer/month     | [GitHub Copilot Business](https://docs.github.com/en/copilot/about-github-copilot/plans-for-github-copilot) at $19/seat/mo as the underlying tool; our recurring layer adds support, not license     |

**Honest caveat**: services-trap risk is real. The Layer 1 cohort program is people-heavy (Vincent + 1–2 coaches per cohort) and doesn't scale linearly without trained coaches. The mitigation is the Agent Lead alumni network as a coach pipeline by year 2 — but if that flywheel doesn't spin, the business caps at a 6–8 cohort/year boutique, which is a fine lifestyle business but not a venture outcome. The Layer 3 recurring revenue is the venture-shaped exit; it depends on Layer 1 graduates wanting ongoing support, which is a real testable assumption.

## What would pressure the thesis

1. **Assumption**: Japanese mid-market engineering buyers will pay ¥10–20M for a 12-week program when they've spent ¥100K/yr on per-seat tooling.
   - **What would pressure it**: First 5 prospects ask for the same engagement at ≤¥3M, or send only 1–2 engineers per cohort.
   - **Lever**: Drop to Candidate B (Agent Lead Bootcamp) as the lead product, treat full-team cohorts as upsell after Lead-installed teams ask.
2. **Assumption**: The English-first / Japanese-language gap is a real adoption blocker, not just a surface complaint.
   - **What would pressure it**: Diagnostic shows engineers are blocked on agent *workflow design* (when to use, how to verify) far more than on *language*. In that case Japan-specificity is a thinner wedge than a global program would be.
   - **Lever**: Reframe as workflow-design enablement that happens to be in Japanese; rebuild curriculum around the universal blockers and de-emphasize the language angle.
3. **Assumption**: Vendor FDE benches and SI consultancies will not staff against the mid-market within 18 months.
   - **What would pressure it**: Anthropic Japan, Cursor Japan, NRI, or NTT Data publicly announces a productized mid-market enablement offer at <¥20M.
   - **Lever**: Pivot to channel partner / certified-trainer status with whoever moves first; surrender the direct-sale motion in exchange for being the named enablement partner.
4. **Assumption**: Coding-agent fluency is a 1–3 quarter skill transfer, not an inherently 2-year senior-engineer-judgment thing.
   - **What would pressure it**: Cohort 1 alumni measured 3 months post-program show no sustained agent-usage lift over baseline.
   - **Lever**: Restructure to a 6-month embedded program (closer to FDE residency) at higher price; abandon the productized cohort framing.

## 2-week experiment

**Bias toward show-don't-tell.** Coding agents in 2026 mean the demoable artifact is itself an installable agent harness customized for a Japanese codebase — not a deck about what we'd build.

**Load-bearing assumption to test**: Will a Japanese engineering 部長 commit to a paid pilot (¥5M+) after seeing a working Japanese-language agent harness running on their actual codebase, in a 60-minute session?

**Artifact to build (week 1)**: A "Japanese-language Claude Code starter pack" — a public GitHub repo containing (a) a `CLAUDE.md` template fully written in keigo Japanese with naming-convention sections for typical Japanese internal codebases, (b) a slash-command set for Japanese code-review etiquette (e.g., `/品質会議準備`, `/レビューコメント整形`), (c) a 5-minute screencast of Vincent using it to ship a real PR end-to-end on a sample manufacturing-domain repo, narrated in Japanese with English subtitles. Built solo in Claude Code in ~5 working days, hosted publicly. Bonus: short LinkedIn post in JP and EN announcing it — distribution test built in.

**Conversations (week 2)**: 6 named Japanese engineering 部長 / 執行役員 / staff engineers from Vincent's network and 1-degree referrals (mix of manufacturing, fintech, telecom). Each conversation opens with a screen-share of the artifact running on a public sample repo, then we ask if we can run it on theirs as a follow-up. Not a deck.

**Specific questions / asks** (asked while looking at the artifact):
1. "Where in this `CLAUDE.md` would you change wording to fit your team's review culture?" — surfaces concrete localization deltas.
2. "If we ran a 12-week version of this on your team for ¥15M, who would I need to convince besides you?" — names the buying committee.
3. "What's currently blocking your team from using Cursor / Copilot more — language, workflow, or trust?" — validates the wedge ranking.
4. "Would you commit to a ¥5M pilot in Q3 if we install it ourselves with one of your repos and one engineer?" — explicit commit ask.

**Pass criteria**: ≥3 ¥5M+ pilot LOIs (or budget-confirmed verbal commits) AND ≥1 buyer pulls out a Q3/Q4 PO date AND artifact gets ≥30 GitHub stars or ≥1 inbound from a Japanese engineering manager Vincent doesn't already know.

**Kill criteria**: 0 LOIs after 6 conversations AND every prospect says the language angle is not their blocker AND the artifact gets <5 stars after 2 weeks of distribution. That's a "not a real wedge" signal.

**Vincent's effort**: ~50 hours total — 30 hours build (artifact + screencast + setup), 20 hours conversations + memo. Output: the public repo, the screencast, a memo with quoted answers from each conversation, and a go / pivot / kill recommendation.

## What we don't know yet

- Whether the buying motion in Japan is closer to ringi-style (12+ weeks, multiple stakeholders, written proposal cycles) or has compressed under AI urgency. This determines whether ¥5–15M pilots are 1-quarter or 3-quarter sales cycles, which dominates capital efficiency.
- Whether the mid-market 部長 buys enablement out of HR/training budget (predictable, slow) or DX/innovation budget (faster, but more political).
- How much of the curriculum has to be re-localized per industry vs. how much is universal Japanese-engineering-culture content. Affects the harness-template moat thesis.
- Whether NEC's CoE expansion will spin out independent-trainer alumni who become competitors or partners.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Anthropic and NEC collaborate to build Japan's largest AI engineering workforce](https://anthropic.com/news/anthropic-nec) — the lighthouse-account anchor that legitimizes the buyer's "we need to do this too" question.
- [GitHub Octoverse 2024](https://github.blog/news-insights/octoverse/octoverse-2024/) — Japan #10 developer geography, 23% YoY growth, baseline market sizing.
- [Nihonium — SaaS adoption in Japan](https://nihonium.io/saas-adoption-in-japan/) — structural-stack data: ~35 apps/company vs. 105 US, 34% SaaS-adopting companies.
- [a16z — Investing in GitButler](https://www.a16z.news/p/investing-in-gitbutler) — tone-setter on "growing portion of all new code is now written by AI agents," validates the trend the program rides.

## Related

- [[Agent Org Design — Senior Operator Partnership]] — adjacent F500/PE-portco bet at the C-suite altitude; Genba is the engineering-team altitude in a different geography.
- [[Torii — Consent and residency gateway for foreign agents calling Japanese enterprise APIs]] — the governance-shaped Japan bet (governance-category kill); Genba is its non-governance sibling.
