---
proto_generator:
  seed: 851838007
  writer: 2
  writers_total: 3
  repo_sha: 29908bd
  generated_at: 2026-04-29T08:00:09+00:00
id: proto-hallmark
aliases:
  - Hallmark
tags:
  - proto
type: proto
status: passed
created: 2026-04-29
origin: ""
---

# Hallmark — Cryptographic agent-attestation gateway that lets enterprise APIs serve verified agent traffic and bill it correctly

## What is it?

**Elevator pitch:** Hallmark is an agent-aware verification gateway that B2B SaaS API providers drop in front of their existing API gateway so they can attribute, meter, rate-limit, and audit per agent-session instead of per shared API key. The buyer pays a per-verified-call fee; in exchange they get a billing/observability feed that finally names the agent, the human it acts for, and the entitlement under which it acted.

**How it works:** The API provider points its public endpoint at Hallmark and ships a tiny verifier library that runs in their existing gateway (Kong, Apigee, Envoy). Agent runtimes — Claude, Cursor, Codex, in-house harnesses — wrap outbound calls with three headers Hallmark defines: a hardware attestation (Intel TDX / TPM-bound key) proving the runtime is what it claims to be, an OAuth Attestation-Based Client Auth JWT (the IETF draft) proving the human delegation chain, and a per-call entitlement claim ("this agent is authorized to read records ≤$10k for tenant 'acme.com'"). Hallmark verifies the chain in <50ms against issuer registries (ANS, the customer's own IdP, EUDI wallets), emits a per-call decision with a tamper-evident audit log, and exposes a billing/rate-limit feed keyed to the agent-session — not the IP, not the shared API key.

## What's the problem?

Every B2B SaaS company is now serving agent traffic from its enterprise customers, but the controls assume humans. The provider currently can't tell three things apart: (a) their paying customer's own authorized Cursor/Claude session calling on the customer's behalf, (b) that same customer's rogue intern script using the same API key to scrape, and (c) a competitor pretending to be the customer through a Claude harness — all three arrive from shared cloud egress IPs with the same shared API key, making IP-based rate-limiting "unworkable" ([Zuplo](https://zuplo.com/blog/rate-limit-ai-agents-beyond-request-counts)). They can't bill per-agent (seats collapse under agents) and can't produce an audit trail that names the agent, the human delegator, and the runtime version. Today they cope by lowering rate limits, banning IP ranges (banning Anthropic), or staring at logs and hoping.

## Why now (2026)

- **The IETF picked an agent-identity standard in March 2026, which collapses fragmentation risk for a gateway built today.** `draft-klrc-aiagent-auth-00` composes WIMSE/SPIFFE for agent identity with OAuth 2.0 for delegation, and the OAuth WG's `draft-ietf-oauth-attestation-based-client-auth-08` provides the on-the-wire JWT format ([IETF AIMS draft](https://datatracker.ietf.org/doc/html/draft-klrc-aiagent-auth-00), [OAuth attestation draft](https://datatracker.ietf.org/doc/draft-ietf-oauth-attestation-based-client-auth/)). A gateway implementing these can credibly claim "future-proof" rather than proprietary.
- **Cloudflare and GoDaddy launched the public-web verification layer in April 2026, but explicitly stop at the public web.** The Cloudflare-GoDaddy partnership shipped Web Bot Auth + Agent Name Service for crawler/agent traffic on the open web ([The Register, 2026-04-07](https://www.theregister.com/2026/04/07/cloudflare_godaddy_ai_bot_blocking)). Critically, ANS verifies *what an agent is* — not who it acts for — anchoring identity to the agent provider's domain ([ANS spec, GoDaddy](https://github.com/godaddy/ans-registry/)). The B2B-API-side equivalent, with delegated-user attestation, is the unfilled half.
- **OAuth itself acknowledges the multi-hop delegation gap.** WorkOS's April 2026 piece quotes the OAuth standard admitting prior-actor claims in delegation chains are "informational only" and not enforced for access control — which is exactly the gap that lets Cross-Agent Privilege Escalation and Agent Session Smuggling work ([WorkOS](https://workos.com/blog/oauth-multi-hop-delegation-ai-agents)). The fix needs to live at the resource server, not just the agent-builder SDK.
- **Hardware-attested TEEs went GA across the major clouds, making attestation cheap enough to put on every API call.** Intel TDX with remote attestation is generally available on Google Cloud Confidential VMs, Azure, and Alibaba; Intel Trust Authority's verifier service has a free tier ([Intel TDX overview](https://www.intel.com/content/www/us/en/developer/tools/trust-domain-extensions/overview.html)). The economics of "prove the harness is what it says" flipped from "research-grade" to "enable a checkbox."
- **Per-seat SaaS pricing is collapsing under agent traffic, which forces every API provider to re-meter on agent-session granularity.** Gartner projects 40% of enterprise SaaS spend will shift to usage- or outcome-based models by 2030, with seat-based revenue share declining from 21% to 15% per Deloitte's 2026 TMT predictions ([SoftwareSeni summary](https://www.softwareseni.com/saas-pricing-is-shifting-from-per-seat-to-usage-and-outcome-what-changes-at-your-next-renewal/)). You can't meter what you can't identify — agent attestation is the prerequisite for the new pricing model.
- **HashiCorp shipped native SPIFFE in Vault Enterprise in late 2025 framing it as "non-human identities including AI agents"** ([HashiCorp, Nov 2025](https://www.hashicorp.com/en/blog/spiffe-securing-the-identity-of-agentic-ai-and-non-human-actors)). The infra primitives Hallmark depends on are already being adopted by the customers Hallmark would sell to.

## Who else is doing this

- **Public-web bot-auth layer** — main player: **[Cloudflare Web Bot Auth + GoDaddy ANS](https://developers.cloudflare.com/bots/concepts/bot/verified-bots/)**. Verifies the agent vendor's identity at the CDN edge using cryptographic challenges and a DNS-anchored registry ([ANS spec](https://github.com/godaddy/ans-registry/)). Solves "is this really ChatGPT" for crawlers and the open web; does not handle delegated-user authority, per-tenant entitlement, or per-agent-session billing for authenticated B2B APIs.
- **Agent-builder OAuth SDKs** — main player: **[Scalekit](https://www.scalekit.com/)**. Others: [Stytch Connected Apps](https://stytch.com/blog/agent-to-agent-oauth-guide/), [WorkOS Pipes](https://workos.com/blog/oauth-multi-hop-delegation-ai-agents). They sell to companies *building* agents and bill the agent builder for tool calls. The B2B SaaS provider whose API is being called is the inverse customer side — not in their motion.
- **Internal MCP governance / shadow-MCP discovery** — main player: **[Proofpoint AI MCP Security](https://www.proofpoint.com/us/products/ai-mcp-security)**. Discovers and governs MCP servers stood up inside an enterprise — defending against internal risk, not serving authenticated agent traffic to external customers.
- **Cloud-vendor-locked agent identity** — main player: **[Google Cloud Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview)** for Gemini Enterprise. SPIFFE-based, ties OAuth user delegation to agent identity, audit-logs both. Locked to Gemini Enterprise + Google Cloud — a neutral gateway that works across Anthropic, OpenAI, Google, and in-house harnesses is exactly what those silos can't be.
- **Generic API gateways** — **[Kong](https://konghq.com/pricing)**, Apigee, Envoy. Excellent at request routing, OAuth, rate-limiting per API key. Have no concept of agent attestation, delegated-user proof, or per-agent-session metering. They're the place Hallmark plugs in, not the competitor.

**Where the opening is**: every existing player picks one of (a) "what agent is this?" at the public-web layer, (b) "how does my agent authenticate to APIs?" on the agent-builder side, or (c) "which of my employees stood up an MCP?" inside the firewall. Nobody sells the API provider a unified verifier for *both* hardware-attested agent identity *and* delegated-user authority *and* per-call entitlement, with per-agent-session metering wired in. The reason no incumbent will close this naturally: Cloudflare's commercial motion runs on the public web (CDN-attached), the agent-OAuth SDKs sell to the wrong customer (the agent builder), Proofpoint sells to security teams not API product teams, and the cloud-vendor identity layers are deliberately walled-garden. The vacant lane is the neutral, multi-cloud, agent-vendor-agnostic gateway sold to *the API provider* as a billing/observability primitive, not as a security checkbox.

## Why us

- **ZK-proofs depth makes the per-call entitlement layer credible without a research hire.** The hardest part of Hallmark's protocol is the per-tenant entitlement claim — encoding "agent may read records ≤$10k for tenant acme.com" so it's verifiable in <50ms at the API edge without leaking the tenant's policy. Vincent's recent multi-part ZK write-up means the cryptographic surface is in-domain, not a hire-ahead-of-need.
- **Amazon AI-evaluation experience maps directly onto the trust-and-audit story enterprise buyers actually demand.** Hallmark's audit log isn't a feature, it's the deal — the buyer's compliance team needs to believe "we can prove which agent did this." Two years leading AI model evals at Amazon means knowing exactly what regression, lineage, and reproducibility evidence a serious enterprise buyer asks for, in the language they use.

## Customer & buyer

- **Customer:** API product manager or platform engineering lead at a mid-to-late-stage B2B SaaS company (Series C–public, $50M–$500M ARR) whose paying enterprise customers are now sending material agent traffic. Concrete examples: Linear, Notion, Hex, Retool, Segment, Twilio, Stripe Issuing.
- **Buyer:** VP Platform / VP Eng with the gateway budget line. ACV: $80k–$300k year 1 (2 cents per verified call, 100M–500M calls/year), expanding into the seven figures as the customer's agent traffic grows. Replaces a budget line that's currently labeled "fraud / abuse / bot mitigation" or sits inside the existing API-gateway spend.
- **Champion:** the senior engineer who is personally tired of explaining to the CFO why a single customer's bill jumped 8x last month, or to the CISO why they had to ban half of Anthropic's IP range to stop one bad customer.
- **ICP test:** "do you have ≥3 enterprise customers whose agent-driven API call volume tripled YoY, and have you had at least one billing or abuse incident in the last 6 months you couldn't attribute to a specific agent?" If yes to both, ICP. If they shrug, not yet.
- **Anti-customer:** consumer apps with no API surface, very small SaaS (<$10M ARR) where rolling your own is cheaper than a contract, and any buyer whose primary concern is "block all bots" — Cloudflare is the right answer for them, not Hallmark.

## Wedge / where we could enter

- **Candidate A — Per-agent metering & abuse attribution for one B2B SaaS API** *(led with billing pain).* Sell the gateway as "you'll finally know which agent is generating this bill, and you'll be able to charge for it." Lands on the platform/eng side, expands to security. Risk: feels like a billing tool, not infrastructure.
- **Candidate B — Compliance-grade audit log for agent-modified records in regulated B2B SaaS** *(led with audit pain).* Land on financial-services / healthcare / legal SaaS where "an agent modified this record" needs to be provable for SOC2, HIPAA, MAR. Risk: longer sales cycle, but stickier.
- **Candidate C — "Agent-traffic rescue" for SaaS APIs that just had a public incident** *(led with reactive pain).* Watch HN/Twitter for "we had to ban Anthropic from our API" stories and DM the eng lead. Smaller TAM but warmer leads.

What would push toward one: which of A/B/C produces the fastest LOI in the 2-week experiment. Default starting bet is A — billing pain is universal across the entire ICP, and "attribute traffic to an agent" is the same engineering primitive whether the buyer's pain is billing, audit, or abuse.

## What makes it defensible

- **(a) Primary — Issuer-registry network effects.** Every agent runtime that integrates Hallmark's headers (Claude, Cursor, OpenAI Codex, Gemini, in-house harnesses) becomes verifiable across every API provider that runs Hallmark. Each new API provider raises the value of the agent integration and vice versa. This compounds the way Stripe's "every merchant accepts cards" did — neutrality is the moat that ANS+Cloudflare can't claim because they're owned by infrastructure incumbents who agent vendors will hesitate to depend on.
- **(b) Secondary — Per-tenant entitlement schemas as a standards body.** Once Hallmark has 20 API providers, the entitlement-claim vocabulary ("read ≤$10k", "modify own-records-only", "no-PII-egress") starts to look like a de facto standard. Whoever owns the schema owns the gravity. Defensible because incumbents either don't care (Cloudflare) or can only standardize within their walled garden (Google, AWS).
- **(c) Year-3 endgame — Be the SWIFT of agent-to-API traffic.** Every agent call between two organizations carries a Hallmark-signed receipt. At that scale, Hallmark is the audit trail of the agent economy and the reference data for any insurance / regulator / dispute resolution downstream of agent commerce.

## How it could make money

| Layer                      | Price range                                | Comparable                                                     |
| -------------------------- | ------------------------------------------ | -------------------------------------------------------------- |
| **Verified-call metering** | $0.20–$2.00 / 1k verified agent calls      | [Kong Konnect: $200/M requests](https://konghq.com/pricing)    |
| **Platform subscription**  | $30k–$200k/yr platform fee + volume        | [Scalekit Growth tier: $49/mo + $0.25/1k overage](https://www.scalekit.com/pricing) |
| **Audit & compliance pack (later)** | $50k–$250k/yr add-on for SOC2/HIPAA-grade tamper-evident logs | Internal pricing of compliance attestation vendors (Drata, Vanta enterprise tiers) |

**Business-model risk:** the buyer might just buy the gateway-plus-attestation function from Cloudflare or Kong as a feature add-on. Counter: Cloudflare's edge is the public web (where the customer is anonymous), and Kong/Apigee don't own agent identity issuers — Hallmark's value is the cross-vendor verifier network, not the gateway code itself. If Cloudflare or Kong ship "agent attestation lite" for free, Hallmark survives by owning the per-tenant entitlement schema and the audit-log layer they won't naturally build.

## What would pressure the thesis

1. **Assumption:** Agent runtimes (Claude, Cursor, OpenAI Codex) will adopt a standard set of attestation headers within 18 months.
   - **What would pressure it:** Anthropic and OpenAI ship competing, incompatible agent-identity headers and refuse to converge. Or one of them ships their own gateway and the others reactively follow with proprietary alternatives.
   - **Lever:** ship a translation layer in Hallmark — "we accept all four formats, the API provider only deals with one." Multi-protocol support becomes part of the value, not a workaround.
2. **Assumption:** The B2B SaaS API provider, not the agent builder, is the buyer with budget and pain in 2026.
   - **What would pressure it:** API providers wait for their gateway vendor (Kong/Apigee) to ship a feature, or for Cloudflare's enterprise tier to extend to authenticated APIs. Buying decision moves from VP Platform back to "wait for our existing vendor."
   - **Lever:** lead with the billing/metering use case (which their incumbent gateway literally cannot do) rather than security. Re-frame Hallmark as a revenue tool, not a security one.
3. **Assumption:** Hardware attestation (TDX/TPM-bound) is acceptable performance overhead on the agent-call path.
   - **What would pressure it:** Attestation latency runs into multi-hundred-ms territory for cold runtimes; agent vendors push back on the per-call cost; or Apple Silicon / non-Intel hardware doesn't ship comparable primitives in time.
   - **Lever:** support a "soft attestation" mode (signed software-runtime claims with audit-log only, no hardware TEE) for low-stakes tiers; reserve hardware-rooted attestation for the compliance pack. Keep the protocol layered.
4. **Assumption:** Enterprise buyers will pay separately for "verified agent identity" rather than treating it as table stakes their existing gateway should provide.
   - **What would pressure it:** Apigee or Kong bundle a "good-enough" attestation feature into their enterprise tier for free as a competitive response.
   - **Lever:** double down on the cross-vendor issuer-registry network effect (which a single-gateway vendor can't replicate) and the entitlement-schema standards play. Be the layer above the gateway, not a gateway.

## 2-week experiment

**Load-bearing assumption to test:** *Will B2B SaaS API product/platform leaders engage with — and sign LOI for — a verified-agent-attestation gateway that lives in front of their existing API gateway, when shown a working demo of attribution + per-agent metering for their actual API?*

**Artifact to build (week 1):** A live demo at `hallmark.dev/demo` showing a real B2B SaaS API (start with the Linear or Notion public API as a stand-in) being called by three agents simultaneously: (a) a legitimate Cursor session under Vincent's authorized account, (b) a "rogue" script using the same API key but no attestation, (c) a "spoofed competitor" using a Claude harness pretending to be Vincent. Hallmark verifies headers in real time and shows a live dashboard: per-agent attribution, per-session billing, an audit row for each call with the chain "agent runtime → human delegator → entitlement". Includes a 5-minute screencast walkthrough plus a public scorecard showing verifier latency (<50ms p99 target) under load. The verifier reference implementation is open source on GitHub for credibility; the dashboard and issuer registry are hosted.

**Conversations (week 2):** 8–12 named API product / platform leads at the ICP — Linear, Notion, Hex, Retool, Segment, Twilio, Vercel, Resend, Cloudflare Workers, Anthropic Console, OpenAI Platform. Mix of warm intros and cold outreach. Each conversation opens with the screencast, then drives into their actual API surface and asks "would you ship this in front of your gateway in Q3?"

**Specific questions / asks** *(answerable in 30 minutes with the artifact open)*:
1. Looking at this dashboard, can you point to the row that resembles your worst recent agent-traffic incident?
2. If we replaced your current rate-limit logic with this attribution feed tomorrow, what would break?
3. What would your billing team need to charge customers per-agent-session instead of per-API-key?
4. Who owns this decision — you, or your existing gateway vendor's account team?
5. Would you sign a design-partner LOI for $X for an 8-week pilot?

**Pass criteria:** ≥3 design-partner LOIs (any non-zero $) AND ≥1 buyer commits to a pilot start date AND ≥75 stars or ≥5 inbound contact requests on the open-source verifier within 14 days of public launch.

**Kill criteria:** 0 LOIs after 12 conversations, OR every prospect says "we'd buy this from Kong/Cloudflare" with no caveat, OR the sub-50ms verifier latency target requires architecture choices that compromise multi-cloud portability.

**Vincent's effort:** ~70 hours total. ~45 hours building the artifact (verifier reference impl, three agent harnesses, dashboard, screencast — coding-agent-leveraged). ~25 hours on outreach, calls, and a written memo. Output: live hosted demo, public GitHub repo, written memo with quoted answers from each conversation, and a go / pivot / kill recommendation.

## What we don't know yet

- Whether the per-call entitlement claim is best expressed as a SNARK (privacy-preserving but computationally heavy), a signed JWT (cheap but leaks the policy shape), or a hybrid — needs prototyping against 2–3 realistic enterprise policies.
- Whether the buyer will object to a Hallmark-hosted issuer registry on data-sovereignty grounds and demand a self-hosted option from day one, which would change the GTM economics.
- How much of the agent-runtime instrumentation needs to be built by Hallmark vs. shipped by Anthropic/OpenAI/Cursor themselves — the former is a longer integration tail, the latter is a partnership negotiation.
- Whether any of the IETF drafts gets superseded or stalled before reaching working-group consensus, which would change the standards-bet calculus.

## Vincent's Feedback

**The "What's the problem" framing is weak and partly misdirected.** The proto leans on three examples — (a) authorized customer agent, (b) customer's rogue intern script, (c) competitor spoofing the customer through a Claude harness. Examples (b) and (c) are customer-side API key hygiene problems, not SaaS-provider problems. The provider bills whoever holds the key. If that's the pitch, this isn't a problem worth a new vendor.

**The strongest provider-side problem is pricing-model migration, not security.** Per-seat pricing assumed humans. When 5 seats fan out into 200 concurrent agent sessions hitting the API 100x harder, the provider serves expensive traffic at flat-rate prices and can't repackage because they can't see how many agents sit behind one key. The Gartner/Deloitte usage-pricing "why now" is the load-bearing one; the rest is dressing. The other real provider-side angle is **selective rate-limiting** — today, throttling a misbehaving agent throttles the whole customer (humans + good agents); the provider wants a scalpel.

**But both of those wedges largely collapse under existing primitives.** Short-lived per-agent child tokens minted from a parent API key already solve per-agent rate-limiting and per-agent metering. The pattern exists and is in production: OAuth Token Exchange (RFC 8693), AWS STS AssumeRole, Stripe restricted keys, GitHub fine-grained PATs, GCP service-account impersonation, HashiCorp Vault child tokens, macaroons. No Hallmark needed for either wedge.

**What honestly remains for Hallmark after this critique:**
1. Most B2B SaaS APIs (Linear, Notion, Hex, Retool) don't expose child-token minting — but that's a feature their gateway can add, not a vendor purchase.
2. Customers won't mint per-agent tokens unless agent runtimes (Claude, Cursor, Codex) ask for them — that's a runtime-convention problem, not a vendor problem.
3. **Cross-vendor identity attestation + tamper-evident audit log for regulated SaaS** — proving "this was genuinely Claude in a TEE under vincent@acme's delegation" for SOC2/HIPAA/MAR audit. This is the only piece a child token can't do, and it's essentially Wedge B in the proto.

**Net read:** the proto's framing is roughly inverted. It leads with the wedge already solved by existing primitives (Wedge A — billing/abuse attribution) and buries the one that actually requires a new vendor (Wedge B — compliance-grade audit for regulated industries). If this comes back into rotation, lead with regulated-SaaS audit, drop the security-spoofing examples, and treat per-agent metering as a side benefit of the audit infrastructure rather than the headline.

## References

- [IETF draft-klrc-aiagent-auth-00 — AI Agent Authentication and Authorization](https://datatracker.ietf.org/doc/html/draft-klrc-aiagent-auth-00) — the AIMS framework that anchors Hallmark's protocol bet.
- [draft-ietf-oauth-attestation-based-client-auth-08](https://datatracker.ietf.org/doc/draft-ietf-oauth-attestation-based-client-auth/) — the OAuth WG's attestation-JWT format that becomes Hallmark's wire format.
- [Cloudflare verified bots docs](https://developers.cloudflare.com/bots/concepts/bot/verified-bots/) — the public-web equivalent that defines the half of the problem Hallmark doesn't try to own.
- [Zuplo on rate-limiting AI agents beyond request counts](https://zuplo.com/blog/rate-limit-ai-agents-beyond-request-counts) — clearest articulation of why IP-based limits and shared API keys collapse under agent traffic.
- [WorkOS on the multi-hop delegation problem](https://workos.com/blog/oauth-multi-hop-delegation-ai-agents) — engineering-grade walkthrough of the OAuth gap Hallmark closes at the resource-server side.
- [HashiCorp on SPIFFE for agentic AI](https://www.hashicorp.com/en/blog/spiffe-securing-the-identity-of-agentic-ai-and-non-human-actors) — the infra primitives Hallmark depends on, already in production.
- [Google Agent Identity for Gemini Enterprise](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) — the cloud-vendor walled-garden version Hallmark differentiates against.

## Related

- [[Whisper — ZK attestation layer for agent-to-API calls so agents prove eligibility without leaking PII]] — adjacent bet, agent-side SDK for user-attribute proofs; Hallmark is the API-provider-side counterpart.
- [[Torii — Consent and residency gateway for foreign agents calling Japanese enterprise APIs]] — same gateway pattern, scoped to APPI/Japan jurisdictional surface.
- [[Veritrace — Cryptographically-attested eval logs that turn enterprise AI compliance from a PDF into a proof]] — sibling bet on cryptographic audit trails as enterprise compliance primitive.
