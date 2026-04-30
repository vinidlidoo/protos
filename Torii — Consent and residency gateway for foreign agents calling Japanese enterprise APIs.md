---
proto_generator:
  seed: 420631118
  writer: 2
  writers_total: 2
  repo_sha: 0a63ec4
  generated_at: 2026-04-28T23:30:26+00:00
id: proto-torii
aliases:
  - Torii
tags:
  - proto
type: proto
status: drafted
created: 2026-04-28
origin: ""
---
# Torii — Consent and residency gateway for foreign agents calling Japanese enterprise APIs

## What is it?

**Elevator pitch**: Japanese enterprises want to expose their APIs (CRM, ERP, custom internal services) to foreign AI agents — Claude, GPT, internal Python harnesses run by US/EU vendors — but their compliance, infosec, and legal teams keep blocking it because nothing on the market answers "which agent, on whose behalf, with what consent, with logs my regulator can read in Japanese." Torii is the gateway that sits in front of those APIs in-country, brokers the OAuth/MCP handshake on Japanese terms, captures APPI-grade consent, keeps personal data resident, and produces a Japanese-language audit trail the buyer's legal team will sign off on.

**How it works**: A Japanese enterprise points its outbound API surface (or its MCP servers) at Torii instead of exposing them directly. Foreign agents authenticate to Torii — not the underlying API — and Torii (a) enforces per-agent, per-tool scopes; (b) captures and re-presents APPI-compliant cross-border consent in the right language for the right data subject; (c) decides what data crosses the border vs. is masked or kept resident; (d) writes a tamper-evident log keyed to the agent identity, the human principal, and the tool call. The compounding value: the buyer's legal team approves once, and every new foreign agent inherits the policy. Each new enterprise customer adds Japanese-specific policy templates, growing the moat for the next sale.

## Why now (2026)

- **APPI applies extraterritorially and is now actively used to block foreign vendors.** Reed Smith confirms APPI "applies to any business...handling personal information of individuals in Japan, regardless of whether the business is physically located in the country," with penalties up to 100M yen ([Reed Smith](https://www.reedsmith.com/our-insights/blogs/viewpoints/102l2yi/japan-in-focus-data-protection-and-ai-in-japan/)). The 2022 amendments expanded this to cover indirect data acquisition — meaning a US-built agent that touches Japanese-resident data via a Japanese SaaS API is in scope ([IAPP](https://iapp.org/news/a/practical-notes-for-japans-important-updates-of-the-appi-guidelines-and-qas)).
- **Cross-border transfer requires named-country consent in Japanese.** APPI requires "prior consent of data subjects specifying the receiving country" — name, applicable laws, and recipient's protective measures — for any non-whitelisted destination, which includes the US ([DLA Piper](https://www.dlapiperdataprotection.com/index.html?t=law&c=JP)). This consent capture is exactly the surface area no agent OAuth provider handles today.
- **Japan's May 2025 AI Promotion Act made the regulator's enforcement model "name and shame," which Japanese boards weight heavier than EU-style fines.** No monetary penalties, but the government can publicly disclose non-compliant operators ([FPF](https://fpf.org/blog/understanding-japans-ai-promotion-act-an-innovation-first-blueprint-for-ai-regulation/)). Reputational risk drives Japanese GCs to over-block foreign agents until the controls are demonstrable.
- **Agent-OAuth is exploding but jurisdiction-blind.** Scalekit, Stytch, WorkOS, and the broader MCP-gateway ecosystem (Proofpoint AI MCP, MintMCP) all ship agent-auth, but none address country-named consent or in-country residency as a first-class concern ([Scalekit](https://www.scalekit.com/), [Stytch agent OAuth guide](https://stytch.com/blog/agent-to-agent-oauth-guide/), [Proofpoint MCP](https://www.proofpoint.com/us/products/ai-mcp-security)). The Stytch guide explicitly punts compliance to the application developer.
- **Japan is structurally underpenetrated in SaaS — the agent wave will hit a market that uses ~35 apps per company vs. 105 in the US ([Nihonium](https://nihonium.io/saas-adoption-in-japan/))**. The agent layer becomes the primary integration interface, so the gateway sitting in front of it captures disproportionate value per dollar of buyer software spend.
- **OAuth for agents is recognized as a hard, unsolved problem on the technical side too.** Scalekit's own architecture write-up frames it as "long-lived delegated authority, not a login flow," with token lifecycle and multi-tenant isolation as the headline challenges — and the entire piece never mentions jurisdiction ([Scalekit on agent OAuth](https://www.scalekit.com/blog/oauth-ai-agents-architecture)). The blind spot is the wedge.

## Who else is doing this

- **Agent-OAuth platforms (US-built, jurisdiction-blind)** — main player: **[Scalekit](https://www.scalekit.com/)**. Others: [Stytch Connected Apps](https://stytch.com/blog/agent-to-agent-oauth-guide/), [WorkOS](https://workos.com/). They solve delegated OAuth, scope enforcement, and audit logs at a US/EU-developer altitude. EU residency is a $99/mo add-on at Scalekit ([pricing](https://www.scalekit.com/pricing)); APPI consent capture and Japan residency are not on any roadmap. They sell to the agent builder, not the enterprise being asked to expose APIs — which is the actual buyer in Japan.
- **MCP gateways and AI-traffic security** — main player: **[Proofpoint AI MCP Security](https://www.proofpoint.com/us/products/ai-mcp-security)**. Discovers MCP servers, governs them through a unified gateway, and logs transaction-level forensics. Built and sold for Fortune-100 US security teams. Does not handle Japanese-language consent capture, name-and-shame-style regulator reporting, or the "sign here in Japanese" buyer-side workflow.
- **Japanese domestic identity / data-residency vendors** — players like NRI, Trend Micro, NTT Data offer enterprise IAM and domestic cloud, but none have shipped an agent-aware product. Their go-to-market is consulting-led, slow, and built for human SSO. They will eventually move, but they're 18–36 months from shipping anything an agent operator can actually integrate against.
- **DIY in-house** — large Japanese enterprises (Sony, Rakuten, MUFG) are building bespoke API gateways with hand-rolled APPI logic. This is exactly the build-vs-buy moment: it works for the first 1–2 agent integrations and then collapses under the maintenance burden as the agent ecosystem fragments across Anthropic, OpenAI, Google, and dozens of in-house harnesses.

**Where the opening is**: the buyer-side gateway sold to Japanese enterprises (not US agent builders), in Japanese, with APPI-as-product-feature rather than a checkbox. US agent-OAuth vendors will not naturally close it because their entire commercial motion runs through US developer-platform sales; their distribution can't reach a Tokyo GC. Japanese SI giants will not naturally close it because their product muscle is decade-late on agent-native integrations. The gap requires somebody who can sell into a Japanese boardroom in Japanese AND ship agent-grade infrastructure in a week — a combination that maps almost uniquely onto Vincent's profile.

## Why us

- **Native-level Japanese plus US tech depth is the actual prerequisite for this bet.** Selling APPI-compliance infrastructure to a Japanese GC requires reading the regulator's Japanese-only Q&A docs, presenting in keigo to a board, and shipping production OAuth/MCP infrastructure — all three. Vincent's 10 years in Japan plus CS/AI depth and coding-agent fluency is a rare profile; most US infra founders fail step 1, most Japanese SI founders fail step 3.
- **France/EU bridgehead is a built-in second market.** Once APPI consent is productized, GDPR cross-border transfer is the same architecture with different policy templates. Vincent's French fluency and 4 years in France gives a credible second go-to-market without a second hire.

## Customer & buyer

- **Customer**: Head of Information Security or Head of Digital Transformation at a Japanese enterprise (1,000–10,000 employees) being asked by a US AI vendor to expose APIs to that vendor's agent.
- **Buyer**: Same role, but signs jointly with the General Counsel / 法務部長. Budget line: information security or compliance, not R&D. Typical ACV $80k–$250k year one, scaling with API call volume and number of foreign agents on the gateway.
- **Champion**: Often a "DX-suishin" (DX promotion) lead who has a US agent vendor's pilot stalled in legal review. They want to unblock the pilot.
- **ICP test**: ≥1 foreign-vendor agent pilot currently stuck in legal/compliance review for ≥60 days, OR an internal AI committee that has explicitly written "no agent access to customer data without APPI controls" into policy.
- **Anti-customer**: Japanese consumer apps with no enterprise customer base — too small a compliance surface to need this. Also US-headquartered companies with a Japan branch — they should buy from Scalekit/WorkOS and bolt on local counsel.

## Wedge / where we could enter

- **Candidate A — Stuck-pilot rescue**: identify 5–10 Japanese enterprises with publicly known AI agent pilots that have stalled (Nikkei xTECH covers these); offer a free 2-week unblock by deploying Torii in front of the API and documenting the consent flow. High intent, low CAC, painful but referenceable wins.
- **Candidate B — US AI vendor channel**: partner with one US agentic AI vendor (e.g., a coding-agent or sales-agent company with Japanese pipeline) to package Torii as the "Japan-ready" version of their product. They sell more, we ride their distribution. Risk: they may eventually build it.
- **Candidate C — Domestic SI partnership**: white-label Torii to NRI or NTT Data as the agent-native module of their compliance suite. Faster scale, slimmer margins, slower brand-building.

What would push toward A: at least 3 of the 10 stalled-pilot accounts respond to outreach within 2 weeks. What would push toward B: a willing US vendor logo emerges who is large enough to matter but small enough to need help. Default to A unless B materializes organically.

## What makes it defensible

- **(a) Primary — policy template library by industry × foreign vendor**: each sale produces a tested mapping of "what consent language clears APPI for vendor X calling tool Y on data class Z." This compounds: customer #20 onboards in days because we already shipped templates for their three target US vendors. A US competitor cannot meaningfully build this without a Japanese policy team in Tokyo.
- **(b) Secondary — buyer-side trust**: GCs at Japanese enterprises share vendors via informal industry councils. The first 5 logos make the next 20 inbound. This is the same dynamic that keeps Salesforce out of mid-market Japanese banking — local trust beats product features.
- **(c) Year-3 endgame — become the de-facto handshake**: every foreign agent vendor that wants to sell into Japan integrates with Torii once, the way they integrate with Stripe for payments. At that point the network effect flips: enterprises buy Torii because every vendor already speaks Torii, vendors integrate Torii because every enterprise expects it.

## How it could make money

| Layer                                    | Price range            | Comparable                                                                                       |
| ---------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------ |
| **Layer 1 — Gateway + audit (per-API)**  | $80k–$250k ACV         | [WorkOS audit logs $125/mo per SIEM + $99/mo per 1M events](https://workos.com/pricing)          |
| **Layer 2 — Per-agent consent broker**   | $0.50–$2.00 per agent-month    | [Scalekit Growth $49/mo + $0.25/1k tool calls; EU residency $99/mo add-on](https://www.scalekit.com/pricing) |
| **Layer 3 (later) — Compliance reports** | $20k–$60k/yr per buyer | [Vanta enterprise plan](https://www.vanta.com/pricing) (custom pricing; tier is the analog)      |

Honest caveat: there is real services-trap risk in year 1. Japanese enterprise sales cycles are long (6–12 months) and the first 5 deployments will pull in Vincent personally for legal walkthroughs. The defense is to ruthlessly turn each engagement's bespoke policy work into a reusable template — if year 2 still requires founder-led legal sessions per deal, we've productized a consultancy, not a product.

## What would pressure the thesis

1. **Assumption**: Japanese enterprises will keep wanting to integrate foreign AI agents (vs. defaulting to all-domestic AI like Sakana, NTT's tsuzumi).
   - **What would pressure it**: a domestic-AI-first procurement mandate from METI or major keiretsu, signaling that the buyer-side problem is "use Japanese AI" not "make foreign AI compliant."
   - **Lever**: pivot the product to broker between Japanese enterprises and Japanese AI vendors — same gateway, different policy library. Slower TAM growth but the architecture survives.
2. **Assumption**: Scalekit / WorkOS / Stytch will not ship deep Japan localization in 18–24 months.
   - **What would pressure it**: any of them announces a Tokyo office with a Japanese GC partnership, or ships APPI consent flow as a first-class feature.
   - **Lever**: race to lock the top 5 Japanese logos and make the policy library the moat; the US vendors can build the auth plumbing but not the policy library or the buyer-side trust.
3. **Assumption**: APPI extraterritorial enforcement actually bites in the next 24 months.
   - **What would pressure it**: regulator stays passive, no high-profile foreign-vendor enforcement case lands.
   - **Lever**: lean harder on "name and shame" reputational risk and on the GDPR-mirror story for EU expansion; broaden from "regulatory must-have" to "buyer-procurement must-have."
4. **Assumption**: Agent-to-API traffic will dominate over agent-to-GUI in enterprise integrations within 3 years.
   - **What would pressure it**: enterprises mostly let agents drive existing GUIs (Anthropic Computer Use style) instead of exposing APIs.
   - **Lever**: extend Torii to broker browser-driven agent sessions too — same consent and audit primitives, different transport.

## 2-week experiment

**Load-bearing assumption to test**: Japanese enterprise GCs / CISOs treat foreign-agent API access as a real, currently-blocked procurement decision — and will pull a Japanese-language consent and audit gateway through legal review faster than a translated US product.

**Artifact to build (week 1)**: a working v0 of Torii deployed on a public domain. Concretely:
- A reverse proxy (Cloudflare Worker + a small Go service) sitting in front of a fake "Japanese SaaS" sample API.
- An OAuth/MCP handshake where a Claude agent (the prospective foreign agent) presents identity, requests scopes, and is held until APPI-compliant Japanese consent is captured from a simulated data subject.
- A Japanese-language audit log export (PDF) suitable for showing to a GC, with the agent identity, principal, scopes, data classes touched, and timestamps.
- A 4-minute screencast in Japanese walking a CISO persona through the flow.

Vincent solo with coding agents in 5 days: yes — this is auth glue + a templated PDF generator + a Japanese-language UI.

**Conversations (week 2)**: 8–12 conversations, all in Japanese, all opened with the screencast or a live demo:
- 4–6 enterprise CISO / DX leads at companies known to have stalled foreign-AI pilots (sourced from public Nikkei xTECH coverage and LinkedIn).
- 2–3 Japanese GCs (via existing Tokyo legal-tech network).
- 2–3 Japanese-market leads at US agentic-AI vendors (Anthropic Japan, Glean Japan, etc.), to test the channel-partner wedge.

**Specific questions / asks**:
1. Watching this flow — is this what your legal team is actually asking for? What's missing?
2. If we deployed this in front of [their stalled pilot], does that unblock the pilot? Who else would need to sign off?
3. What would you pay per year for this if it cleared one stalled vendor? Two? Five?
4. (Vendor channel only) If we white-labeled this as "[your product] for Japan," would you pay for the wrapper or expect us to monetize the enterprise side?
5. Which competitor would you compare us to in your procurement document?

**Pass criteria**: ≥3 enterprise design-partner LOIs (paid or unpaid) AND ≥1 buyer names a budget line and PO timeline AND screencast generates ≥30 inbound signals (LinkedIn DMs, replies, X follows from Japanese AI/security accounts).

**Kill criteria**: <2 enterprises express intent to deploy AND every conversation surfaces "we'd rather wait for [Scalekit/Proofpoint/NRI] to ship a Japanese version" AND no GC will commit to a written legal review of the artifact.

**Vincent's effort**: ~80 hours total — 40 hours build (heavy coding-agent leverage), 40 hours conversations + memo. Output: hosted live demo URL, GitHub repo (or selectively private), memo with quoted answers from each conversation, and a go / pivot (channel-partner) / kill recommendation.

## What we don't know yet

- Whether the right wedge is gateway-in-front-of-API (B2B infra sale) or compliance-as-a-service (legal/audit sale to GCs). The technical artifact is the same; the GTM is very different.
- Whether large Japanese enterprises will accept a SaaS gateway at all, or insist on on-prem from day one (which changes ACV, deployment cost, and sales cycle).
- Whether there's a parallel play with Korean enterprises (PIPA), which would change the early-customer mix and validate the policy-library moat sooner.
- How fast Anthropic / OpenAI / Google will ship their own jurisdiction-aware consent layers natively into their agent APIs — if they do, Torii needs to live above them as a buyer-side policy and audit layer, not below them as auth plumbing.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Practical notes for Japan's important updates of the APPI guidelines and Q&As — IAPP](https://iapp.org/news/a/practical-notes-for-japans-important-updates-of-the-appi-guidelines-and-qas) — the authoritative read on what 2022 APPI amendments actually changed for foreign operators.
- [Japan in focus: Data protection and AI in Japan — Reed Smith](https://www.reedsmith.com/our-insights/blogs/viewpoints/102l2yi/japan-in-focus-data-protection-and-ai-in-japan/) — clearest English-language summary of APPI extraterritoriality and the May 2025 AI Promotion Act.
- [Understanding Japan's AI Promotion Act — Future of Privacy Forum](https://fpf.org/blog/understanding-japans-ai-promotion-act-an-innovation-first-blueprint-for-ai-regulation/) — useful framing of "name and shame" enforcement model that drives Japanese board behavior.
- [SaaS Adoption in Japan — Nihonium](https://nihonium.io/saas-adoption-in-japan/) — baseline numbers on how thin the Japanese SaaS layer is, which is why the agent layer becomes the integration substrate.
- [OAuth for AI Agents — Scalekit architecture writeup](https://www.scalekit.com/blog/oauth-ai-agents-architecture) — frames the agent-OAuth problem in detail; the absence of jurisdiction is itself the signal.

## Related

- (none yet — first proto in this jurisdictional-agent-infra cluster)
