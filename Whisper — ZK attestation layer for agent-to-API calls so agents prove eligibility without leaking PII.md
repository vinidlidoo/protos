---
proto_generator:
  seed: 455901942
  writer: 1
  writers_total: 2
  repo_sha: 5106d57
  generated_at: 2026-04-28T21:12:07+00:00
id: proto-whisper
aliases:
  - Whisper
tags:
  - proto
type: proto
status: drafted
created: 2026-04-28
origin: ""
---

# Whisper — ZK attestation layer for agent-to-API calls so agents prove eligibility without leaking PII

## What is it?

**Elevator pitch:** Whisper is a developer SDK + hosted prover that sits between AI agents and the APIs they call. When an API needs to know "is this user a verified adult, a US-resident accredited investor, KYC'd, not on OFAC, has $X in account," Whisper lets the agent attach a short zero-knowledge proof of that fact pulled from the user's wallet or a trusted issuer — instead of forwarding a passport photo, a bank statement, or a session token that leaks everything else. Compliance teams at the API side get a cryptographic "yes" with an audit trail; the model provider never sees the raw PII.

**How it works:** The user authorizes the agent once, binding their EUDI wallet, ZKPassport, or issuer-signed credentials to the agent session. When the agent hits a participating API, the API responds with a Whisper attestation challenge ("prove user is 18+, EU-resident, not on EU sanctions"). The agent's runtime calls Whisper's prover (local for small predicates, hosted enclave for heavy ones), produces a SNARK, and replays the request with the proof in a header. The API verifies in <50ms against Whisper's verifier library, logs the proof hash for audit, and serves the call. Value compounds because each predicate Whisper standardizes (age, jurisdiction, KYC tier, balance threshold, license-held) becomes reusable across every agent and every API in the network.

## Why now (2026)

- **Agent-to-API traffic is becoming the default surface for SaaS, and existing auth wasn't designed for it.** MCP went from experimental release in late 2024 to de-facto agent protocol in 18 months, but its [authorization spec](https://modelcontextprotocol.io/specification/2025-11-25) only standardizes OAuth 2.1 + PKCE for *connecting* — it explicitly leaves "downstream authentication" and agent-to-agent identity propagation as ["organization specific" gaps](https://stackoverflow.blog/2026/01/21/is-that-allowed-authentication-and-authorization-in-model-context-protocol/). Today every API team is reinventing this badly.
- **Agent-paid API calls are being standardized as a primitive, which makes agent-side identity material.** Cloudflare and Coinbase launched the [x402 Foundation](https://blog.cloudflare.com/x402/) in September 2025 to make machine-to-machine payments a native HTTP-layer behavior, with Cloudflare shipping native x402 support in their Agents SDK and MCP integrations. The natural next question for any API operator accepting x402 traffic is "who's the human behind this agent, and are they allowed to buy this?" — and x402 itself doesn't answer it.
- **The EU has put a regulatory clock on selective-disclosure identity.** Every member state must ship an [EU Digital Identity Wallet](https://ec.europa.eu/digital-building-blocks/sites/spaces/EUDIGITALIDENTITYWALLET/pages/694487738/EU+Digital+Identity+Wallet+Home) by end of 2026, with built-in selective-disclosure ("prove age without revealing birth date"). That gives every EU citizen a wallet that can issue ZK predicates — but no standard layer yet for agents to actually consume them at API call time.
- **The cryptographic primitives finally work in production at agent latency.** [ZKPassport](https://docs.zkpassport.id/faq) generates ICAO-9303 passport proofs entirely on-device in seconds; [Privado ID](https://docs.privado.id/docs/introduction/) offers a production-grade verifier SDK for off-chain and on-chain checks. Two years ago "ZK identity" was a research demo; today it's an SDK call.
- **High-profile AI data leaks are now an each-quarter event, and buyer demand for "data minimization at the agent layer" is no longer hypothetical.** Privacy regulators are increasingly framing "the agent forwarded the user's raw passport to a US LLM provider" as a GDPR/CCPA violation in the making; the cheapest mitigation is to never forward it.

## Who else is doing this

- **ZK identity wallets / SDKs (consumer-facing)** — main players: **[ZKPassport](https://zkpassport.id/)** (NFC passport scan, on-device proofs) and **[Privado ID](https://www.privado.id/)** (formerly Polygon ID; W3C VC + SNARK stack). They solve the *issuance and proof generation* side beautifully, but they're aimed at dApps and Web3 verifiers — neither ships a verifier middleware aimed at SaaS APIs receiving agent traffic, and neither addresses MCP / x402 agent contexts.
- **Agent identity / proof-of-personhood** — main player: **[World AgentKit](https://world.org/blog/announcements/now-available-agentkit-proof-of-human-for-the-agentic-web)** (zk-linked agents to verified humans, integrating with x402). World answers "is there a unique human" but not "what is that human authorized to do" — predicates beyond uniqueness are out of scope.
- **Traditional KYC/identity APIs** — main player: **[Sumsub](https://sumsub.com/pricing/)** ($1.35–$1.85 per verification publicly listed); other large incumbents are Persona and Onfido. These are server-side: the API operator pulls the user's documents and stores them. They are exactly the architecture Whisper inverts; they will not voluntarily move to a model where they no longer hold the data.
- **Agent payment / commerce rails** — main player: **[x402 Foundation](https://blog.cloudflare.com/x402/)** (Cloudflare + Coinbase). x402 standardizes payment but punts on identity; their roadmap explicitly leaves "who is the buyer" to other layers.
- **MCP gateway / authorization vendors** — emerging space (Aembit and others writing about [MCP + OAuth](https://aembit.io/blog/mcp-oauth-2-1-pkce-and-the-future-of-ai-authorization/)). They focus on token brokering and scope, not on cryptographically attested user attributes.

**Where the opening is.** Two adjacent ecosystems are converging — agent runtimes (MCP, x402) and ZK identity wallets (EUDI, ZKPassport) — but no one owns the *predicate layer* that translates "this API call requires X about the user" into "the agent attached a verifying SNARK." Wallet projects won't build it because their buyer is the consumer; KYC incumbents won't build it because it cannibalizes their data-custody business model; agent-runtime projects won't build it because it's a vertical-specific compliance problem they want to push out. That's the seam.

## Why us

- **Vincent has done a multi-part public ZK write-up and continues active study, plus three years at Amazon fusing heterogeneous data sources via knowledge graph.** That combination is rare: most ZK people are cryptographers who haven't shipped enterprise integrations, and most data-fusion engineers don't read SNARK papers. Whisper requires both — designing the predicate schema *and* shipping a verifier SDK that compliance teams will actually adopt.
- **Tri-cultural fluency (EN/FR/JA) maps directly to the three jurisdictions where this regulation lands first** — EU (eIDAS 2 wallet), Japan (My Number digital ID push), US (state-by-state age-verification laws). Selling cross-jurisdictional compliance tooling rewards someone who can sit in a Tokyo legal review meeting in JP, then a Paris GDPR debrief in FR.

## Customer & buyer

- **Customer:** Platform/API engineering lead at a B2B SaaS that already gets MCP/agent traffic and has a regulated data attribute (age-gate, KYC tier, jurisdiction, license, balance) gating some API calls. Think a fintech data API, a regulated commerce API, an alcohol/age-gated content API, an EU-resident-only data feed.
- **Buyer:** Head of Compliance or CISO with a privacy-engineering line item. Typical ACV: $40k–$120k yr 1, growing with predicate volume.
- **Champion:** A staff platform engineer who has been quietly horrified that their MCP server logs contain user passport JPEGs forwarded by Claude/Cursor/etc., and has tried and failed to convince leadership it's a problem.
- **ICP test:** ≥1 regulated attribute gating an API endpoint AND existing or planned MCP server AND someone in legal has flagged "agents forwarding PII" in the last 6 months.
- **Anti-customer:** Pure-consumer apps with no regulated-data gating — Whisper is overkill. Also web3-native projects already standardized on Privado ID — duplication, not value.

## Wedge / where we could enter

- **Candidate A — EU age-gate for agent-driven content/commerce APIs.** EUDI wallet ships end-2026; a thin "prove ≥18 + EU-resident from your EUDI wallet to my API" SDK is the most concrete v1, riding the regulator-imposed wallet rollout. Push toward this if early conversations confirm EU SaaS feels deadline pressure.
- **Candidate B — Fintech KYC-tier proofs for agent-driven trading / DeFi-adjacent APIs.** Agents need to prove "user is KYC'd to tier 2, accredited, not OFAC" to call sensitive endpoints. Higher ACV, sharper pain, but longer compliance review cycle. Push toward this if a design partner has an active "we're getting agent traffic and don't know if it's allowed to trade" incident.
- **Candidate C — MCP-server hardening kit for any vertical.** Sell directly to the platform team running an MCP server: "drop in our verifier middleware, your server stops accepting raw PII in tool calls." Fastest distribution but weakest wedge — risks being a feature, not a product.

Default to A unless B's first 5 conversations surface a willing-to-pay design partner faster.

## What makes it defensible

- **(a) Primary — predicate schema & verifier-network effects.** Every API that adopts Whisper standardizes on its predicate schema (EU-resident, KYC-tier-2, age-≥18, balance-≥X). Once 5–10 APIs in a vertical share predicates, agents only need to prove each predicate once per session and reuse across calls. That makes Whisper the cheapest path for both new APIs (free agent-side adoption) and new agents (free API-side adoption) — classic two-sided lock-in.
- **(b) Secondary — issuer integrations and the cryptographic glue between wallets and APIs.** Wiring EUDI wallet, ZKPassport, Privado ID, US state mDLs, and bank-issued credentials into one verifier interface is unglamorous integration work that compounds: every new issuer multiplies what every existing API verifier accepts.
- **(c) Year-3 endgame — the audit-and-compliance ledger.** Every Whisper proof produces a hashed, timestamped attestation that satisfies "we never saw the underlying PII but we have cryptographic proof of eligibility at call time." That ledger becomes the artifact compliance teams reach for under audit, which makes ripping Whisper out cost six-figure compliance-rework even after technical alternatives appear.

## How it could make money

| Layer                           | Price range            | Comparable                                                                                   |
| ------------------------------- | ---------------------- | -------------------------------------------------------------------------------------------- |
| **Verifier SDK + per-proof**    | $0.10–$0.40 per proof  | [Sumsub per-verification $1.35–$1.85](https://sumsub.com/pricing/) (we displace at 5–10× lower because no document storage) |
| **Hosted prover + predicate library** | $2k–$10k/mo platform   | [Privado ID issuer/verifier hosting](https://docs.privado.id/docs/introduction/) (positioned as identity-as-a-service)             |
| **Compliance ledger + enterprise SLA (later)** | $40k–$120k/yr | [Sumsub enterprise plan](https://sumsub.com/pricing/) (custom enterprise pricing in this band)                                |

**Honest caveat.** Per-proof pricing has a chicken-and-egg risk: until enough APIs verify Whisper proofs, agent runtimes won't bother attaching them; until agents attach them, APIs see no value paying for the verifier. The wedge (a single vertical, EU age-gate) exists specifically to bootstrap one side first. Services-trap risk is real if early customers want bespoke predicate work — keep predicate library tightly scoped and refuse one-offs.

## What would pressure the thesis

1. **Assumption:** Compliance teams will accept ZK proofs as legally equivalent to seeing the underlying document.
   - **What would pressure it:** Regulators (CNIL, BaFin, FinCEN) issue guidance that explicitly requires the verifier to retain the source document. Or a court decision rejects ZK attestation as "insufficient diligence."
   - **Lever:** Pivot toward augmentation rather than replacement: Whisper proof becomes the *first-line check* and a fallback document-storage path remains for high-risk transactions. Reframe value as audit-trail + fraud-reduction, not data-minimization alone.

2. **Assumption:** Agent runtimes (MCP, x402, OpenAI Agents SDK) standardize on a verifier-middleware pattern within 12–18 months — i.e., there's a hook to attach proofs in agent calls.
   - **What would pressure it:** OpenAI/Anthropic ship a competing "AgentAuth" spec that bakes identity attestation into the protocol itself, removing the need for a third-party SDK.
   - **Lever:** Pivot from SDK-vendor to predicate-schema steward + reference verifier — sell the *standardized predicates and audit ledger* even if the protocol layer becomes commodity.

3. **Assumption:** Buyers will pay per-proof rather than expect this as a free open standard.
   - **What would pressure it:** EUDI wallet ecosystem ships an open verifier reference implementation that's "good enough" for free.
   - **Lever:** Move value up-stack to the compliance ledger + multi-issuer integration tier; concede commodity verification to open-source and price the audit-grade SLA.

4. **Assumption:** The traffic mix justifies a vertical solution — i.e., a non-trivial fraction of API calls genuinely involves regulated user attributes that today travel as raw PII.
   - **What would pressure it:** Survey of 20 MCP-server-running SaaS shows <10% of tool calls touch regulated attributes; the rest are read-only data fetches.
   - **Lever:** Narrow target market hard to fintech + age-gated + EU-data-residency verticals; abandon horizontal MCP-hardening framing.

## 2-week experiment

**Load-bearing assumption to test:** A platform engineer at a B2B SaaS already running an MCP server, when shown a working Whisper integration in 5 minutes, will agree the data-leakage problem is real, will name a specific predicate they'd want to verify, and at least 3 of 10 will sign an LOI for a pilot.

**Artifact to build (week 1):** A public, hosted demo + open-source SDK in one repo:
1. A toy MCP server with one tool that requires "user is ≥18 and EU-resident."
2. A reference agent client (TypeScript) that calls the tool, gets a 402-style "predicate required" response, requests a proof from a mock EUDI wallet emulator, and replays the call with a SNARK header.
3. The server's verifier middleware checks the proof in <50ms and logs an attestation hash.
4. A hosted live demo at `whisper.dev/demo` that any visitor can fork-and-run; a 4-minute screencast walking through it; a one-page docs site explaining the predicate schema. Use existing ZK toolchains (Noir / Circom / snarkjs) — Vincent does *not* implement novel cryptography in 5 days; he implements credible glue.

**Conversations (week 2):** 10 platform/compliance leads — sourced via INSEAD network, the ZK community, MCP server maintainers list, and 3 cold-emails to fintechs known to ship MCP. Open every call by sharing the live demo URL on screen, then ask the questions below while they click around it.

**Specific questions / asks:**
1. Look at this MCP tool call log — does this look like what your server logs contain today?
2. If our SDK could replace the raw PII forwarded here with a verifying proof, what's the *first* predicate you'd want? (looking for: age, jurisdiction, KYC tier, balance, license)
3. Who in your org owns the decision to add a new agent-side authentication layer? (looking for: named title, single owner, not a committee)
4. What proof format would your compliance team accept as evidence of eligibility-at-call-time?
5. If we showed up Monday with a 2-week paid pilot for predicate X, would you sign? What's missing for that to be a yes?

**Pass criteria:**
- ≥3 design-partner LOIs in writing AND
- ≥1 buyer names a budget line and a quarter for a paid pilot AND
- demo repo gets ≥50 GitHub stars OR ≥1 inbound from an MCP/x402 ecosystem maintainer.

**Kill criteria:**
- 0 LOIs after 10 conversations, OR
- ≥7/10 buyers say "we don't actually log raw PII through MCP" (problem is hypothetical), OR
- ≥3/10 say "we'd just use Persona/Sumsub for this" and meaningfully push back on the data-minimization framing.

**Vincent's effort:** ~50 hours total. ~30 hours building the demo + SDK with coding agents (the SNARK pieces leverage existing libraries — Vincent's job is integration and DX). ~15 hours on outreach + conversations + memo. ~5 hours on the screencast and landing page. **Output:** the public demo repo + hosted page, a memo with quoted answers from all 10 conversations, and a go / pivot / kill recommendation.

## What we don't know yet

- Whether MCP / x402 maintainers would accept Whisper as a reference predicate-attachment standard or fight it as fragmentation.
- The actual prover latency budget agents tolerate per call — is 200ms a hard ceiling, or do users tolerate 1s for sensitive actions?
- Which jurisdiction's regulatory clock is *actually* the binding one for early buyers (EU eIDAS rollout vs US state age-verification laws vs Japan My Number).
- Whether issuer-side relationships (EUDI member-state wallets, US bank-issued credentials) are gettable in year 1 or require political capital we don't yet have.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Aztec — ZKPassport case study](https://aztec.network/blog/zkpassport-case-study-a-look-into-online-identity-verification) — concrete production deployment of consumer ZK identity (Sybil resistance for validators).
- [Cloudflare — Launching the x402 Foundation](https://blog.cloudflare.com/x402/) — primary source on how agent payment rails are being standardized (the layer Whisper rides above).
- [Stack Overflow Blog — Authentication and authorization in Model Context Protocol](https://stackoverflow.blog/2026/01/21/is-that-allowed-authentication-and-authorization-in-model-context-protocol/) — third-party analysis of the gaps in MCP authorization that Whisper sits on top of.

## Related

- [[Study/]]
- [[Protos/]]
