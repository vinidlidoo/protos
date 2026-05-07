---
id: proto-tuner
aliases:
  - Tuner
tags:
  - proto
type: proto
status: drafted
created: 2026-05-04
origin: ""
proto_generator:
  seed: 714033580
  writer: 1
  writers_total: 1
  repo_sha: ddb0091
  generated_at: 2026-05-04T20:15:34+00:00
---

# Tuner — Replay your last week of agent decisions through a proposed playbook change before merging it

## What is it?

**Elevator pitch.** Tuner is a GitHub App for engineering teams whose coding agents have become first-class committers. When someone proposes a change to your `CLAUDE.md`, `AGENTS.md`, or `.cursor/rules/*` playbook, Tuner replays the last 7 days of real agent decisions — every PR opened, ticket triaged, review comment posted by Copilot cloud agent, Cursor background agents, or Claude Code subagents — through the proposed playbook and shows the diff: which decisions would have flipped, which would have been better, which would have been worse. The buyer is the platform team that owns the playbook; the customer is every engineer whose agent the playbook governs.

**How it works.** Tuner installs as a GitHub App on the repo. It captures the full provenance of each agent decision — the prompt, the tools called, the diff produced, the human accept/revert outcome — into a private decision log. When you open a PR that touches an agent-config file, Tuner's CI check forks N replay environments (one per recent decision), re-runs each through the new playbook with the original tool surface mocked from the captured trace, and renders a side-by-side report: the deltas the change would have produced if it had shipped 7 days ago. Approve or block before merge.

## What's the problem?

Engineering orgs have committed playbook files (`CLAUDE.md`, `AGENTS.md`, `.cursor/rules/`) that govern a measurable share of merged code, triaged tickets, and PR reviews — but no one knows what changing a line in those files actually does to agent behavior in the wild. Today the workflow is: someone PRs a rule change, two reviewers eyeball it, it merges, behavior shifts somewhere downstream, and a week later a senior engineer notices the agent stopped writing tests or started rewriting unrelated files. The blast radius is invisible at PR time. Teams currently mitigate by being slow to change rules at all — which is the wrong outcome, because rules need to evolve as the codebase does.

## Why now (2026)

- **The artifact teams need to test against now exists, is real, and is at scale.** `AGENTS.md` is the Linux-Foundation-stewarded cross-agent format that already has [60k+ examples on GitHub](https://agents.md/), with first-class adoption from Codex, Cursor, Aider, Gemini CLI, and the GitHub Copilot coding agent. Anthropic's [`CLAUDE.md` memory docs](https://code.claude.com/docs/en/memory) describe it as "markdown files that give Claude persistent instructions for a project, your personal workflow, or your entire organization." The unit of regression — a versioned, repo-scoped behavior config — is now standard.
- **The agent itself is now a first-class committer with a tracked decision history.** GitHub's Copilot cloud agent ships with usage metrics that include "the number of pull requests created by Copilot cloud agent that have been merged" and "median time to merge for merged pull requests, including pull requests created by Copilot cloud agent" ([docs](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent)). The replay corpus Tuner needs — agent decisions with PR-lifecycle outcomes — is a server-side artifact GitHub already emits.
- **Multi-agent fleets are now first-party, not script-glue.** GitHub Copilot's cloud agent supports "specialized custom agents for different tasks" with per-agent custom instructions ([source](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent)), and Cursor's Pro tier ships ["Cloud agents"](https://www.cursor.com/pricing) alongside MCPs, skills, and hooks. The number of distinct agents whose behavior depends on the same playbook file has gone from 1 to >5 in a single repo, multiplying the regression surface.
- **Live X discourse confirms there is no formal CI for these files yet.** A May-2026 Grok-x-search synthesis on engineering-team practices around `CLAUDE.md`, `AGENTS.md`, and `.cursor/rules/` returned the explicit summary: "No formal CI yet: emerging; relies on manual/human + agent reviews rather than automated pipelines." The behavioral failure modes are reported repeatedly — drift, multi-agent chaos, security/prod risks on rule changes — and the gap is named.
- **The eval-on-PR pattern is already commercially priced.** Promptfoo offers ["CI/CD integration — Run evals automatically on every PR"](https://www.promptfoo.dev/docs/getting-started/) as a productized pattern; Cursor's [Bugbot](https://cursor.com/pricing) charges "$40 / user / mo" to review "up to 200 PRs/mo." Buyers already pay for AI judgment-on-PR; Tuner extends that pattern to a class of artifact (the playbook) those tools don't cover.

## Who else is doing this

- **General-purpose LLM eval platforms** — main player: **[Braintrust](https://www.braintrust.dev/pricing)** ($249/mo Pro). Others: [LangSmith](https://www.langchain.com/pricing-langsmith) ($39/seat/mo Plus), [Humanloop](https://humanloop.com), [Promptfoo](https://www.promptfoo.dev/docs/getting-started/) (open-source). They evaluate prompt and model changes against test datasets you curate. They do not own the playbook artifact, do not capture agent decisions in production with provenance, and are oriented around request/response pairs not multi-agent decision trajectories.
- **AI-on-PR review tools** — main player: **[Cursor Bugbot](https://cursor.com/pricing)** ($40/user/mo, 200 PRs/mo). Others: GitHub Copilot's auto-review feature, [CodeRabbit](https://www.coderabbit.ai), Greptile. These review *code* PRs for bugs; they do not specifically reason about *playbook* PRs and have no decision-replay mechanism.
- **Agent observability / tracing** — main player: **[LangSmith](https://www.langchain.com/pricing-langsmith)**. Others: [Braintrust](https://www.braintrust.dev/pricing), Helicone, Arize Phoenix. They capture traces and let you slice metrics; they don't bind traces to a versioned playbook artifact or run a counterfactual replay against a proposed config change.
- **Platform-native rule customization** — main player: **[GitHub Copilot custom instructions](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent)**. Others: Anthropic's [`CLAUDE.md` + auto-memory](https://code.claude.com/docs/en/memory). The platforms ship the artifact but explicitly leave behavior verification to the user — Anthropic's own docs note that "Claude treats them as context, not enforced configuration… how you write instructions affects how reliably Claude follows them." There is no first-party regression harness, and the platforms have a structural reason not to ship one (it would make their non-determinism visible and quantifiable).

**Where the opening is.** The eval platforms own the test-set/prompt-pair surface; the AI-PR tools own code-bug review; the observability tools own the trace. None of them treat the playbook file (`AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`) as the unit of regression, and none of them replay captured production decisions through a proposed config change. That artifact-centric framing — "the playbook is the system; what would have happened if last week ran on the new playbook" — is the wedge no incumbent will naturally close, because closing it requires being model-agnostic and platform-neutral (you have to replay across Copilot, Cursor, and Claude Code traces in the same view), which cuts against every incumbent's distribution motion.

## Why us

- **Vincent led AI model evaluations at Amazon for 2 years and has direct exposure to how large orgs measure AI quality, regression and risk.** The replay-against-captured-traces methodology is the same shape as a regression-eval harness for production AI; the credibility, vocabulary, and design-partner conversations transfer directly.
- **Vincent ships end-to-end with coding agents.** This bet's product surface — a GitHub App + replay engine + decision-trace capture — is exactly the artifact a solo founder armed with Claude Code can build a working v0 of in 5 days, and the bet's whole thesis is that agent-management is the new core skill — Vincent has lived it daily.

## Customer & buyer

- **Customer:** the platform/devex engineer who owns the org's `AGENTS.md` / `CLAUDE.md` and is responsible for "agent quality" as a metric.
- **Buyer:** Director of Engineering or VP Platform/DevEx at a 100–1000-engineer company where coding agents already merge ≥10% of PRs. Budget line: developer-experience tooling. Typical ACV: $25k–$150k depending on agent volume.
- **Champion:** the senior engineer who got paged because an `AGENTS.md` edit changed agent behavior in production and wants a guardrail before it happens again.
- **ICP test:** ≥3 distinct coding agents in active use (Copilot cloud + Cursor + Claude Code), ≥1 committed playbook file with >10 commits in the last quarter, and ≥1 incident ticket whose root cause was a rule-file change.
- **Anti-customer:** solo developers and <20-engineer teams — agent volume is too low for replay deltas to be statistically interesting, and the buyer doesn't exist.

## Wedge / where we could enter

- **Candidate A — Claude Code-only first.** Single integration target (`CLAUDE.md` + Claude Code subagent traces from the project's `~/.claude/projects/<project>/` directory or Anthropic Workbench logs); fastest to ship, narrowest ICP. Push toward this if early conversations show Claude Code is the agent doing the most committing.
- **Candidate B — GitHub Copilot cloud agent first.** Use the Copilot cloud agent's PR-lifecycle metrics API as the decision corpus and `AGENTS.md` as the playbook; biggest TAM, more friction to ingest cross-vendor traces. Push toward this if early conversations show Copilot cloud agent is the dominant first-class committer at the buyer.
- **Candidate C — `AGENTS.md`-stewarded multi-agent first.** Position as the cross-vendor harness from day one (Linux-Foundation-stewarded format means the artifact is genuinely shared); harder to bootstrap because each agent's trace ingestion is a separate integration. Push toward this if buyers explicitly say their pain is "Cursor and Copilot disagree on the same `AGENTS.md`."

Default to (A) for the 2-week experiment because it's the only one a solo founder can ship a meaningful v0 of in 5 days. (B) and (C) are roadmap.

## What makes it defensible

- **(a) Primary — owning the playbook as the unit of regression.** Every customer's decision corpus accumulates in our store with provenance binding (playbook commit SHA, agent vendor, tool calls, outcome). The longer a customer runs, the higher-resolution their replay set; the methodology lives at the intersection of "production trace" and "versioned config" that no incumbent owns. This is the moat to lead with — it's also the answer to the obvious investor objection ("won't GitHub or Anthropic just ship this?"), because the cross-vendor replay surface is structurally adversarial to a single platform owner.
- **(b) Secondary — captured trace dataset compounds.** Every replay produces a labeled (decision, playbook-version, outcome) tuple — a revealed-preference dataset of which playbook edits actually move agent behavior in which directions. This is the kind of artifact that becomes a benchmark, then a recommender ("teams like yours that added rule X saw Y% fewer revert-after-merge events").
- **(c) Year-3 endgame — the policy layer for agent fleets.** Once we own the regression surface, we own the proposing surface — Tuner suggests playbook edits before the engineer writes them, drawing on the cross-customer dataset. That converts a pure CI gate into a governance product without becoming the security/compliance vibe Vincent specifically avoids.

## How it could make money

| Layer                                   | Price range            | Comparable                                                                              |
| --------------------------------------- | ---------------------- | --------------------------------------------------------------------------------------- |
| **Layer 1: per-seat CI gate**           | $30–$60/user/mo        | [Cursor Bugbot](https://cursor.com/pricing) at $40/user/mo                              |
| **Layer 2: trace ingestion + storage**  | $1.50–$3 per 1k traces | [LangSmith](https://www.langchain.com/pricing-langsmith) at $2.50/1k base traces        |
| **Layer 3 (later): platform tier**      | $50k–$200k ACV         | [Braintrust](https://www.braintrust.dev/pricing) Enterprise, LangSmith Enterprise tiers |

The honest business-model risk: per-seat pricing inverts under heavy agent fan-out (the seat is the human reviewer, but the work being gated is the agent's). We'd need to watch ACV/seat ratios in early customers and shift to consumption pricing on traces if seat counts undershoot.

## What would pressure the thesis

1. **Assumption: the playbook file is genuinely load-bearing for agent behavior.**
   - **What would pressure it:** if early replays consistently produce <5% behavioral delta on real playbook commits, the file is decoration and the regression product has nothing to gate.
   - **Lever:** widen the unit of regression to include skill/subagent definitions, MCP server configs, and hook scripts — the surrounding agent-config surface that *is* load-bearing.
2. **Assumption: replay against a captured trace is methodologically sound for multi-turn agent decisions.**
   - **What would pressure it:** if replay diverges from real-world behavior by turn 3-4 on average (the Auralis-class methodology kill — multi-turn replay of static traces collapses), the deltas Tuner reports aren't predictive.
   - **Lever:** narrow the scope to "terminal-decision" replay — score on the outputs that actually matter (PR opened? files touched? tests added?) rather than on intermediate agent dialogue. Trade fidelity for predictiveness.
3. **Assumption: the platform owners (GitHub, Anthropic, Cursor) won't ship a first-party version that obviates Tuner.**
   - **What would pressure it:** GitHub or Anthropic announcing a native "rule-change preview" feature that shows behavior deltas before merge.
   - **Lever:** the cross-vendor replay surface is the structural defense — the moment one platform ships a single-vendor version, our pitch sharpens to "and you also use the other two." Ship cross-vendor before any platform owner ships single-vendor.
4. **Assumption: the trace-ingestion path stays open at the agent platforms.**
   - **What would pressure it:** Anthropic, Cursor, or GitHub closing programmatic access to the per-decision trace data we need for replay (similar to how Twitter closed the firehose).
   - **Lever:** trace-capture-via-GitHub-App on the artifact side (PR diffs, comments, issue events are all on GitHub) — gives us platform-independent ground truth at the cost of some intermediate-trajectory fidelity.

## 2-week experiment

**Load-bearing assumption to test:** that platform/devex engineers at orgs running coding-agent fleets will pay for a CI gate that replays last-week-of-agent-decisions through a proposed playbook change — and specifically, that the deltas Tuner surfaces are *useful enough to act on*, not just numerically interesting.

**Artifact to build (week 1):** a working v0 GitHub App, deployed publicly, that does the following on a curated demo repo where Claude Code subagents are committing real PRs daily:
1. Captures every Claude Code decision (PR opened, file edits, test runs) with the `CLAUDE.md` SHA active at decision time.
2. On any PR that touches `CLAUDE.md`, posts a CI check with: "Replayed N decisions from the last 7 days through the proposed `CLAUDE.md`. K would have changed: [diff view per decision]."
3. Public dashboard at tuner.dev or similar: "the last 30 replays we ran on this open-source repo, classified."

Solo, 5 working days of build. Stack: GitHub App in TypeScript, replay engine wrapping Anthropic API with the captured tool-call sequence as the user-message track, results stored in SQLite and rendered as a static dashboard.

**Conversations (week 2):** 8–12 platform/devex leads at companies that publicly use Claude Code or Copilot cloud agent at scale (Anthropic, Vercel, Stripe, Shopify, Replit, Sourcegraph, Linear, Sentry — DevEx Slack and "platform-eng" Twitter are the recruitment channel). Each conversation opens with the live demo on the buyer's own repo if they'll provide read access to a `CLAUDE.md` + recent PR history, otherwise on the public demo.

**Specific questions / asks:**
1. Looking at this replay output: would you want this CI check on your repo's `CLAUDE.md` PRs?
2. Of the deltas surfaced here, which would have changed your decision to merge?
3. What's the closest internal tool you've built or considered building for this?
4. If we shipped this for Claude Code only, would you pay for it before we add Copilot/Cursor coverage?
5. What's the ceiling on per-seat pricing for a CI gate at your org?

**Pass criteria:** ≥3 design-partner LOIs from companies meeting the ICP test, AND ≥1 buyer pulls out a PO date within 90 days, AND the public dashboard hits ≥100 GitHub stars OR ≥3 inbound DMs from platform engineers asking to install on their repo.

**Kill criteria:** <2 LOIs after 12 conversations, OR every buyer says "we'd want this but only if it covers Copilot cloud agent first" (signals a different MVP — possibly worth pivoting to (B), but signals against (A) shipping fast).

**Vincent's effort:** ~50 hours build (week 1 — solo with Claude Code), ~25 hours conversations + memo (week 2). Output: live GitHub App + public demo dashboard + memo with quoted answers + go/pivot/kill recommendation including which of A/B/C the conversations push toward.

## What we don't know yet

- Whether captured Claude Code traces from `~/.claude/projects/` contain enough fidelity to replay decisions with reasonable counterfactual accuracy, or whether we need first-party Anthropic API trace ingestion to make the replay sound.
- How often `CLAUDE.md` / `AGENTS.md` files actually change at the kind of orgs we'd target — if it's <2 commits/quarter, the CI gate is too low-volume to be a daily-active tool.
- Whether the platform team buyer will pay before there's a clear "we shipped a bad rule and Tuner caught it" public incident — i.e., whether this needs a Granola-style incident before adoption flips, or whether the proactive pitch lands.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]]
- [[Touchstone — Per-variant evals so the bespoke-software era doesn't ship a million silently-wrong internal tools]]
- [[Auralis — Private regression-eval harness for enterprise voice-agent fleets where the buyer's own recorded calls are the eval set]]
- [[Agent Org Design — Senior Operator Partnership]]
