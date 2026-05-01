---
proto_generator:
  seed: 30654284
  writer: 1
  writers_total: 2
  repo_sha: 2a7d0ef
  generated_at: 2026-04-30T19:32:00+00:00
id: proto-lodestar
aliases:
  - Lodestar
tags:
  - proto
type: proto
status: passed
created: 2026-04-30
origin: ""
---

# Lodestar — Personal context graph that lets every AI agent operate on an early-stage investor's own taste, deals, and passes

## What is it?

**Elevator pitch**: A solo seed/Series-A partner buys Lodestar so that every AI tool they use — Claude, Cursor, ChatGPT, their CRM's built-in agent — answers as if it has read every memo they've ever written, every deal they passed and why, every founder intro they took, and every check they wrote. Today those tools each maintain their own siloed memory; the partner has to re-explain their thesis dozens of times a week and still gets generic synthesis. Lodestar gives them one private context graph their agents share.

**How it works**: Lodestar runs as a local-first daemon on the partner's laptop and ingests the partner's revealed-preference artifacts — calendar, email, Notion/Drive memos, CRM exports (Affinity/Attio), Slack DMs with founders, Substack inbox — into a typed knowledge graph (deals × people × theses × outcomes × calendar events). Edges carry signed timestamps and the source artifact's hash. The graph exposes itself via a hosted [Model Context Protocol](https://modelcontextprotocol.io/) endpoint scoped to the partner; any MCP-aware tool (Claude, Cursor, Affinity's MCP server, etc.) gets cross-tool memory of *this specific investor's* taste with one config line. Vincent's job is the heterogeneous-source fusion under the typed schema, the local-first daemon, and the MCP server that exposes typed query primitives ("show me deals I passed in the last 18 months whose pass-reason cited team risk and that have since raised an A").

## What's the problem?

The 2026 early-stage partner runs three to five AI tools daily and each one starts cold. Affinity's hosted MCP gives Claude access to *the firm's CRM rows* but not to the partner's pass-memos, the call notes that lived in Granola, the threads with co-investors, or the Substack the founder writes that the partner has been reading for six months. Claude itself ships project-scoped memory but [each project has its own separate memory](https://claude.com/blog/memory) — and nothing crosses between Claude, Cursor, and ChatGPT. The partner's coping mechanism today is to paste a 1,500-word "here's how I think about this market" preamble into every new chat, then accept that the answer still misses obvious context they shared three months ago.

## Why now (2026)

- **MCP is the real cross-tool standard, not aspirational.** Claude, ChatGPT, Cursor, and Visual Studio Code all ship MCP clients today, making "build once, integrate everywhere" actually work for personal context ([source](https://modelcontextprotocol.io/)).
- **Affinity, the dominant VC CRM, just shipped a hosted MCP server in its Scale tier ($2,300/user/year)** — proving incumbents see MCP as the agent-era surface, but exposing only firm-wide CRM rows rather than partner-personal context ([source](https://www.affinity.co/product/affinity-pricing)). The seam is below them.
- **Anthropic shipped memory in September 2025 and rolled it to Pro/Max in October**, validating that frontier-lab memory is a category, but explicitly scoping it per-project per-product — which leaves a cross-tool gap they will not close because each lab wants memory to be a moat, not a portable substrate ([source](https://claude.com/blog/memory)).
- **Local-first personal-data substrates are crossing into agent territory.** Birdclaw, a local SQLite store for a user's tweets/bookmarks/DMs that exposes "scriptable JSON for agents and automation," has 452 stars in months and explicitly markets itself as the agent-readable layer for personal X data ([source](https://github.com/steipete/birdclaw)). The shape of the substrate is being established by individual builders before any platform owns it.
- **VC sourcing is already a "your network is the moat" job.** 4Degrees cites that "80%+ of VC and PE deals are sourced from firm networks" — the asset Lodestar amplifies is exactly the asset partners already believe is decisive ([source](https://www.4degrees.ai/)).

## Who else is doing this

- **VC-purpose CRMs with bolted-on AI** — main player: **[Affinity](https://www.affinity.co/product/affinity-pricing)** ($2,000–$2,700 per user/year). Others: **[4Degrees](https://www.4degrees.ai/)**, **[Attio](https://attio.com/pricing)** ($29–$86/user/month, horizontal but adopted by VC firms like USV per the customer logos on its pricing page). They model deals and contacts; Affinity now ships a hosted MCP server. None of them carry the partner's personal pass-memos, reading history, or Slack DMs — they're firm-shared CRMs and rightly scope themselves to data the firm collectively owns.
- **VC sourcing/data platforms with their own AI agents** — main player: **[Harmonic](https://harmonic.ai/)** with its "Scout — AI agent made for investors" and a "purpose-built MCP" exposing Harmonic's proprietary startup database. Their MCP feeds *external market data* into the partner's agent; Lodestar feeds the partner's *own taste* into the same agent. Complementary, not competitive.
- **Frontier-lab native memory** — main players: **[Anthropic memory](https://claude.com/blog/memory)** (project-scoped, single-product), ChatGPT memory, Cursor memory. Each is a per-product, opt-in, often-summarized layer designed to make their own product stickier. None expose a portable personal context graph.
- **Personal-data substrates and local-first tools** — main player today: **[birdclaw](https://github.com/steipete/birdclaw)** (local SQLite for tweets, "scriptable JSON for agents"). The shape is right (local-first, agent-readable, user-owned) but the surface is one data source, not a fused multi-source graph keyed by the user's professional life.

**Where the opening is**: Every layer above is either (a) firm-scoped, source-of-record CRM that won't cross into private email/Slack/notes, (b) lab-scoped memory that won't cross between products, or (c) single-source local stores. The unowned middle is a *personal*, *cross-source*, *cross-tool* context graph that lives on the user's machine, exposes itself via MCP, and is built around a high-value professional segment whose revealed-preference artifacts are unusually rich and unusually hidden today. CRM vendors won't go here because the graph spans data they don't host (Slack DMs, Granola transcripts, personal Substack inbox); labs won't go here because cross-product portability undercuts their stickiness moat; horizontal personal-AI plays (Mem, Limitless) won't pick a vertical sharp enough to make the schema do real work.

## Why us

- **Heterogeneous-source fusion via a typed knowledge graph is exactly the shape of the Amazon work.** Vincent built an internal trend-analytics product that fused heterogeneous data sources via a knowledge graph. The schema-design taste — what to type, what to leave free-text, where edges carry timestamps vs. weights — is the rare unfair-advantage skill here, and it's the part most LLM-native competitors get wrong by treating context as "all the documents in a vector store."

## Customer & buyer

- **Customer**: solo or small-team early-stage partner (seed → Series A), 1–4 investing professionals at the firm, doing ≥30 first meetings/month and writing ≥5 IC memos/quarter.
- **Buyer**: same person. Pays from the firm's tooling budget alongside Affinity ($2K-$2.3K/user/year) and Harmonic ($contract); any line item below their existing Affinity seat is a checkbook-not-a-procurement decision.
- **Champion**: the partner themselves; this is a single-user purchase by design (no IT review, no security committee — local-first daemon, no firm data leaving the laptop unless they opt into hosted MCP).
- **ICP test**: (1) currently runs ≥3 distinct AI tools (e.g., Claude + Cursor/Replit + ChatGPT) weekly, (2) maintains personal pass-memos in Notion/Drive/Granola outside the firm CRM, (3) has bounced an LLM off "remind me why I passed on X" in the last month and gotten a generic answer.
- **Anti-customer**: large multi-stage funds where the buying decision is firm-wide (procurement/IT enters, security review kills the local-data story, Affinity/DealCloud expansion captures the budget); operators using AI for non-investing knowledge work (the schema isn't sharp for them in v1).

## Wedge / where we could enter

- **Candidate A (lead)**: ship the local daemon + MCP server with three connectors — Gmail, Affinity export, and Granola transcripts — and a single hero query: *"Given a new founder intro, surface every prior interaction, every adjacent deal I passed on or invested in, and every reason text I wrote that's relevant."* The artifact is a 90-second screencast of Claude answering this from a real partner's data.
- **Candidate B**: instead lead with the *passes* corpus alone (one connector: a Notion/Drive folder of pass-memos), and ship the MCP server that lets Claude/Cursor query it. Smallest possible v0; useful for the partner inside 24 hours of install.
- **Candidate C**: integrate as an "Affinity sidecar" — install once, sync from Affinity's API, layer pass-memo + Slack-DM context on top of the firm CRM, expose merged MCP. Highest distribution, highest dependency on Affinity tolerating a sidecar.

What pushes us toward A vs B: whether the first three design partners describe their pain as *"I have a meeting in 20 minutes and I can't remember why I passed on a similar deal"* (A wins — multi-source matters from day one) or *"I have a folder of 200 memos I never re-read"* (B wins — the surfacing alone is the unlock).

## What makes it defensible

- **(a) Primary: typed-graph schema co-evolved with the partner's workflow.** The moat is not the model and not the data — it's the schema decisions that turn raw email/CRM/Slack into a queryable representation of how *this kind of professional* thinks. Each design-partner cycle compounds this: every new query pattern they actually run sharpens the typed primitives the MCP server exposes, which makes Lodestar more useful per partner-hour invested. Generic horizontal personal-AI tools cannot match this without picking a vertical.
- **(b) Secondary: switching cost from a personally-curated graph.** Two years in, the partner has corrected hundreds of edges, added deal-specific properties, and built MCP-prompt habits around the typed primitives. Walking away means re-bootstrapping cross-tool context from scratch — a tax measured in months of the partner's productivity, not in CSV exports.
- **(c) Year-3 endgame**: the schema productizes for adjacent verticals where the same "fragmented professional, valuable revealed-preference artifacts, MCP-aware tool stack" pattern holds — solo M&A advisors, independent equity research analysts, executive coaches, IP attorneys. Each vertical re-uses the daemon and MCP layer; only the schema and connectors change.

## How it could make money

| Layer                           | Price range                     | Comparable                                                                                                           |
| ------------------------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Layer 1: Personal seat**      | $1,200–$2,400/user/year         | [Affinity Essential](https://www.affinity.co/product/affinity-pricing) at $2,000/user/year                           |
| **Layer 2: Hosted MCP + sync**  | $2,400–$4,800/user/year         | [Affinity Scale (with hosted MCP)](https://www.affinity.co/product/affinity-pricing) at $2,300/user/year             |
| **Layer 3 (later): Firm graph** | $25K–$80K/year ACV (5–15 seats) | [Affinity small-team ACV](https://www.vendr.com/marketplace/affinity) ($15K–$45K for 5–15 seats per Vendr's dataset) |
**Load-bearing assumption to test**: that an early-stage partner, given 30 minutes with a working Lodestar reading their actual data through Claude, will (a) reach for a question they've never asked an LLM before because it was always too much context to paste, and (b) say "I'd pay for this today."

**Artifact to build (week 1)**: a working v0 — local daemon (Rust or TypeScript), three connectors (Gmail OAuth, Affinity API, a Notion folder of memos), a typed graph in DuckDB, an MCP server exposing 4–6 query primitives (`deals_by_thesis`, `passes_by_reason_text`, `interactions_with_person`, `co_investor_pattern`, `temporal_neighborhood`, `recent_intros`). Plus a 90-second screencast of Claude using these primitives on Vincent's own data (calendar + Notion + Substack) to answer a non-trivial question. Doable solo with coding agents in 5 working days; the screencast is the conversation prop.

**Conversations (week 2)**: 6 early-stage partners (target list: 2 from the Vincent-Seattle network, 2 cold-outbound to seed-firm Twitter regulars, 2 warm intros via X). Each call opens with the screencast. Then we install a sandboxed Lodestar pointed at *one* connector (their Notion pass-memos folder) live, and ask them to query it through their own Claude instance for 15 minutes.

**Specific questions / asks**:
1. Show me you using your existing AI tools for an investing question right now. *(Establishes baseline.)*
2. Now query the same thing through Lodestar. Tell me what's different.
3. Walk me through the last three deals you passed on. What would you have wanted Claude to say back to you when you first opened those threads?
4. If this existed at $200/month, what's the test that would make you pay vs. cancel after a month?
5. Where would you not let it run? Which data source is too sensitive?

**Pass criteria**: ≥4 of 6 partners actively use the live install for ≥10 minutes unprompted (artifact-driven), AND ≥3 of 6 explicitly ask "when can I install this on my real data" (intent), AND ≥1 verbal LOI for paid pilot at ≥$200/month.

**Kill criteria**: ≥3 of 6 say "Claude memory will eat this in a year, I'll wait," OR no partner can name a question they'd ask Lodestar that they don't already get an acceptable answer to from generic Claude + paste.

**Vincent's effort**: ~50 hours week 1 (build, mostly with coding agents — daemon scaffold + connectors + DuckDB schema + MCP server + screencast), ~20 hours week 2 (6 conversations × 60min including prep + write-up). Output: the artifact (private Loom + GitHub repo); a memo with quoted partner answers; a go/pivot/kill recommendation against the criteria above.

## What we don't know yet

- Whether the right primary connector beachhead is Gmail (universal, messy) or Affinity export (clean, narrow) or Granola (highest signal, smallest install base).
- What the typed schema looks like at the level of "investment thesis" — is a thesis a node, an edge property, a separate document type, or all three for different query shapes?
- Whether MCP's auth model is robust enough today for a partner to expose their personal context graph to multiple AI clients without leaking it cross-context.
- Whether "Affinity sidecar" is a relationship Affinity tolerates (helpful — they sell more seats because their CRM gets more useful) or fights (hostile — we re-expose their data through our MCP).

## Vincent's Feedback

1. **Kill, not pass-on-mission. Granola has eaten this thesis with a smarter wedge.** Granola raised $125M Series C at $1.5B (March 2026), explicitly framing themselves as a professional context layer with meetings as the wedge, has shipped MCP server + cross-meeting Chat + Personal/Enterprise APIs + Spaces, and is going firm-scoped to solve the governance landmine. Lodestar as proposed is 3 years late with a worse wedge and no capital advantage. Future protos should screen against active unicorns with the same thesis before drafting — the writer cited Granola but didn't recognize it as the dispositive competitor.
2. **Wedge-choice principle: pick a single high-signal source with clean consent gating, not heterogeneous fusion from day one.** Granola's "press record on meetings" is a discrete trust ask; Lodestar's "ingest your email + Slack + Notion + CRM + Substack" is a compounding one. The single-source wedge is also a sharper artifact for design-partner conversations. Future protos in personal-AI/memory categories should be challenged on "what's the single highest-signal source you'd ship first" before approving a fusion architecture.
3. **The "who owns the graph when the partner switches firms" question is load-bearing for any personal-context-graph idea targeting employees.** Granola is solving this via firm-scoped Spaces + Enterprise tier. Top-3 risk that was absent from the proto's "what we don't know yet."
4. **Granola is the canonical comp for any "professional context layer" proto from now on, not Affinity.** Affinity is the firm-CRM incumbent with a defensive MCP; Granola is the context-layer-native unicorn with the offensive roadmap. Future protos in this category should benchmark trust-ask, wedge, pricing, and governance posture against Granola.

## Related

- [[Hallmark — Cryptographic agent-attestation gateway that lets enterprise APIs serve verified agent traffic and bill it correctly]]
- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]]
- [[Tessera — Fit-confidence API for agent-mediated apparel commerce trained on smart-glasses body capture]]
