---
proto_generator:
  seed: 851838007
  writer: 3
  writers_total: 3
  repo_sha: 29908bd
  generated_at: 2026-04-29T08:00:09+00:00
id: proto-veil
aliases:
  - Veil
tags:
  - proto
type: proto
status: passed
created: 2026-04-29
origin: ""
---

# Veil — Privacy-preserving authorization mandates for AI checkout agents

## What is it?

**Elevator pitch:** Veil is a merchant-side SDK + hosted verifier that lets AI shopping agents prove "I am authorized by a real human to spend up to $X on category Y, and the human meets the merchant's eligibility rules" without sending the merchant the human's identity, credit limit, or purchase history. Merchants drop a 30-line snippet into checkout; agents attach a zero-knowledge proof to the AP2 / Stripe SPT / Visa Trusted Agent payload they already send. The merchant sees a green checkmark and a hashed attestation it can show an auditor, nothing more.

**How it works:** When a human authorizes an agent (via their wallet, their bank, or a Veil mobile app), Veil issues a signed credential containing the authorization scope (category whitelist, per-merchant cap, expiry) and any eligibility predicates the human chooses to make provable (age, country of residence, employer-sanctioned vendor list, corporate budget tier). At checkout, the agent's runtime calls Veil's prover to produce a SNARK that says "all of {merchant's required predicates} are true for the human backing me, AND this purchase fits within scope" — without revealing which credentials were used or the underlying values. The merchant's verifier checks the proof in <100ms and proceeds with the existing AP2/SPT payment flow. Veil sits *above* the payment rails: they move the money, we make the authorization predicates verifiable without disclosure.

## What's the problem?

Every major agentic-commerce protocol shipping in 2026 — Google AP2, Stripe Shared Payment Tokens, Visa Trusted Agent Protocol, Mastercard Agent Pay — solves the *payment* side: scoped tokens, signed mandates, agent-network registration. None of them solve the *authorization* side privately. The agent must reveal the human's full intent ("buy ≤$120 running shoes for John Doe, address X, age 34, corporate-card holder") to the merchant and the network; the merchant must trust that the agent isn't lying about who's behind it; the human must trust that every merchant the agent visits gets a permanent, queryable record of their delegated purchase authority. Today's "fix" is contract clauses and audit logs. That doesn't survive 100M agents per day or one viral data leak.

## Why now (2026)

- **The payment-rail layer for agentic commerce just got built — but it's transparency-by-default, which makes the privacy gap a real product hole.** Google announced [AP2 in September 2025](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol) with cryptographically-signed Intent and Cart Mandates that create non-repudiable audit trails of every authorized purchase. Stripe shipped [Shared Payment Tokens in December 2025](https://stripe.com/blog/agentic-commerce-suite) as scoped grants over the customer's payment method. Both are merchant- and issuer-trusting by design — neither even mentions ZK or selective disclosure.
- **AI-driven retail traffic is exploding fast enough that "we'll do compliance later" stops working.** Visa cited [a 4,700% surge in AI-driven traffic to U.S. retail websites](https://investor.visa.com/news/news-details/2025/Visa-Introduces-Trusted-Agent-Protocol-An-Ecosystem-Led-Framework-for-AI-Commerce/default.aspx) when launching its Trusted Agent Protocol (October 2025). Adobe documented an earlier [1,200% jump from generative AI sources to U.S. retail in February 2025](https://blog.adobe.com/en/publish/2025/03/17/adobe-analytics-traffic-to-us-retail-websites-from-generative-ai-sources-jumps-1200-percent), with traffic doubling roughly every two months — and Visa [launched Intelligent Commerce Connect on April 22, 2026](https://techafricanews.com/2026/04/22/visa-inc-launches-intelligent-commerce-connect-to-power-ai-driven-payments/) to power AI-driven payments.
- **The big players are explicitly punting privacy primitives downstream.** [Google donated AP2 to the FIDO Alliance](https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/), positioning it as a community-led standard so others build on top. [Visa's Trusted Agent Protocol](https://corporate.visa.com/en/sites/visa-perspectives/newsroom/visa-unveils-trusted-agent-protocol-for-ai-commerce.html) is built on HTTP Message Signatures + Web Bot Auth — agent-identity, not predicate-privacy. [Microsoft's Agent Governance Toolkit](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/) (April 2026) ships DIDs and trust scoring, no ZK. The seam is wide and intentional.
- **Agent authorization is the OWASP top concern, not just a privacy concern.** Prompt injection remains [LLM01 in OWASP's GenAI 2025 top-10](https://genai.owasp.org/llmrisk/llm01-prompt-injection/), and the new [OWASP Top 10 for Agentic Applications](https://nhimg.org/complete-guide-to-the-2026-owasp-top-10-risks-for-agentic-applications) (December 2025) ranks Agent Goal Hijacking #1. Cryptographically-bound, narrowly-scoped authorization is the primary mitigation everyone agrees on but nobody ships at the merchant boundary.
- **The cryptographic primitives are finally fast enough.** [Reclaim Protocol](https://www.reclaimprotocol.org/) has shipped 3M+ zkTLS verifications. [Privado ID](https://www.privado.id/) ships a production verifier SDK with zero-knowledge proofs. The 2024 question "can ZK identity work in production?" has been answered yes.

## Who else is doing this

- **Payment-rail agentic commerce stacks** — main player: **[Google AP2](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol)** with 60+ partners. Others: **[Stripe Agentic Commerce Suite + SPT](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens)**, **[Visa Trusted Agent Protocol](https://developer.visa.com/capabilities/trusted-agent-protocol)**, [Coinbase x402](https://world.org/blog/announcements/now-available-agentkit-proof-of-human-for-the-agentic-web). They establish the rails but treat the authorization payload as cleartext signed mandates — they do not minimize disclosure. Veil rides on top.
- **Agent-identity / proof-of-personhood** — main player: **[World AgentKit](https://world.org/blog/announcements/now-available-agentkit-proof-of-human-for-the-agentic-web)** (March 2026, ZK-linked agents to a verified human via World ID). Others: [OpenAgents AgentID](https://openagents.org/blog/posts/2026-02-03-introducing-agent-identity), [Indicio Proven AI](https://indicio.tech/blog/proven-ai-kyc/), [Strata's "agentic identity"](https://www.strata.io/blog/agentic-identity/new-identity-playbook-ai-agents-not-nhi-8b/). They answer "is there a unique human" and "what is this agent" — not "is the human's purchase scope provably within the merchant's required predicates."
- **ZK identity / verifiable credentials** — main players: **[Privado ID](https://www.privado.id/)** (formerly Polygon ID, W3C VC + ZK stack) and **[Reclaim Protocol](https://www.reclaimprotocol.org/)** (zkTLS for web data attestation, 3M+ verifications). They build the wallet/credential side beautifully but ship to dApp / Web3 verifiers; neither has a checkout-merchant SDK or a payments-rail integration.
- **Traditional KYC / identity verification** — main players: **[Persona](https://withpersona.com/)** ([~$0.43–$0.54 per government-ID check from buyer-reported pricing](https://www.pricelevel.com/vendors/persona/pricing)), Onfido, Sumsub. These are document-custody architectures — exactly what Veil inverts. They will not voluntarily move to a model where they no longer hold the documents.

**Where the opening is.** The payment-rail giants are racing to define *who* an agent is and *what* it can spend, but their architecture deliberately keeps the human's scope and eligibility legible to the merchant — that is the simplest path to enterprise compliance buy-in for them. Wallet/ZK projects own the cryptography but sell to consumers and dApps, not to retail checkout teams. Identity-verification incumbents have the merchant relationship but a business model that requires holding the data. The seam is a merchant-facing verifier that sits atop existing payment rails (AP2, SPT, Trusted Agent), accepts proofs from any wallet, and gives compliance teams a hashed audit trail without ever touching the underlying PII. No incumbent is naturally positioned to close it.

## Why us

- **Vincent has a recently-published multi-part write-up on ZKPs plus active study of the cryptography stack, alongside two years at Amazon running AI model evaluations and one in internal product consulting.** That blend is rare: most ZK practitioners haven't shipped enterprise compliance integrations, and most enterprise compliance vendors don't read SNARK papers. Veil's hardest problem is *predicate schema design* — picking the right 8–12 reusable predicates that compose across merchants, wallets, and jurisdictions. That is a classification problem dressed as a cryptography problem; the AI-evals + ZK-study combo maps unusually directly.
- **Seattle base puts Vincent inside one of the deepest enterprise-payments + AI talent pools** (Amazon, Stripe engineering offices, Microsoft AI security, Convoy/Concur alums for the buyer-side relationships). Distance to design partners is short.

## Customer & buyer

- **Customer:** Head of Checkout / VP Payments at a mid-large e-commerce or marketplace platform with ≥$500M GMV that already accepts AP2 or Stripe SPT traffic and has had a privacy/legal review flag agent-driven purchases.
- **Buyer:** Same role + Head of Privacy / Deputy CISO co-signing. Budget line: existing fraud-and-compliance infrastructure or new "AI risk" envelope. Typical ACV: $60k–$200k yr 1, scaling with agent transaction volume.
- **Champion:** Staff payments engineer who has read the AP2 spec, noticed the Intent Mandate is plaintext, and is uncomfortable that every agent purchase will write the human's full intent into the merchant's database forever.
- **ICP test:** Accepts ≥1 of {AP2, Stripe SPT, Visa Trusted Agent} traffic AND has a legal/privacy memo from the last 12 months flagging agent-purchase data retention AND ≥1 EU buyer demanding GDPR data-minimization for agent flows.
- **Anti-customer:** Pure-DTC brands with no agent traffic yet, or any merchant that *wants* full intent visibility for personalization (we'd be subtracting value, not adding).

## Wedge / where we could enter

- **Candidate A — EU-jurisdiction predicate kit for AP2 merchants.** As the EUDI wallet rolls out and AP2 merchants get EU traffic, ship a "prove EU-resident, age ≥18, GDPR-eligible, within parental-consent rules for under-18" kit that drops into the AP2 flow. Regulator-driven pull, sharp predicate scope, EUDI gives us a free wallet substrate. Push toward this if early EU merchant conversations surface deadline pressure.
- **Candidate B — Corporate-card eligibility for B2B agent purchasing.** Agents buying on behalf of employees need to prove "this purchase category is whitelisted by my employer, within per-vendor cap, employee is still active" without leaking the employer's full procurement policy to every SaaS vendor. Brex, Ramp, AmEx Business as channel; sharp pain (current state is shared-secret API keys); higher ACV. Push toward this if a finance-tools partner offers co-marketing.
- **Candidate C — Age-gating for high-risk verticals (alcohol, gambling, adult, regulated retail).** Narrowest problem, fastest sale, but smallest market and risks being a feature.

Default to A unless B's first 5 conversations surface a willing-to-pay design partner faster, with a Brex- or Ramp-shaped channel partner emerging.

## What makes it defensible

- **(a) Primary — predicate schema network effects across merchants and wallets.** Every merchant that adopts Veil standardizes on its predicate library (age-≥18, EU-resident, KYC-tier-N, employer-whitelisted-vendor, per-merchant-spend-cap). Once a few large merchants and a few wallets accept the same schema, agents only need to assemble proofs once per session and reuse across the full network. New wallets ship Veil-compatible attestations to access the merchant base; new merchants adopt Veil to access the existing wallet base. Two-sided lock-in.
- **(b) Secondary — issuer integration moat.** Wiring EUDI wallet, World ID, Privado ID, US state mDLs, bank-issued KYC credentials, and corporate procurement systems into a single merchant-facing verifier is unglamorous compounding integration work; each new issuer multiplies what every Veil-using merchant accepts.
- **(c) Year-3 endgame — the compliance audit ledger.** Every Veil proof produces a hashed, timestamped attestation that lets a merchant tell an auditor "we proved the buyer met all required predicates without ever holding the PII." That ledger becomes the artifact compliance teams reach for; ripping Veil out becomes a six-figure compliance-rework decision even when technical alternatives exist.

## How it could make money

| Layer                                                | Price range           | Comparable                                                                                                                                                                                                 |
| ---------------------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Per-verification at checkout**                     | $0.05–$0.20 per proof | [Persona government-ID at ~$0.43–$0.54](https://www.pricelevel.com/vendors/persona/pricing) — we are 2–4× cheaper because we do not handle or store documents                                              |
| **Hosted prover + predicate library**                | $3k–$15k/mo platform  | [Stripe Radar for Fraud Teams at $0.05–$0.07 per screened transaction](https://stripe.com/radar/pricing) — analogous checkout-side add-on; Veil bundles per-month rather than per-transaction at this tier |
| **Compliance audit ledger + enterprise SLA (later)** | $60k–$200k/yr         | [Privado ID enterprise support](https://www.privado.id/) (custom enterprise contracts; no public list price, ZK identity is the closest peer)                                                              |

**Honest caveat.** Two-sided cold-start risk: until enough merchants verify Veil proofs, agent runtimes won't bother attaching them; until agents attach them, merchants see no reason to pay for the verifier. The wedge (one jurisdiction or one vertical) exists specifically to bootstrap one side first. Per-verification pricing also creates a margin race-to-the-bottom risk if Visa/Mastercard ship a "free" privacy primitive bundled with their tokens — mitigation is the audit-ledger layer, which is hard for them to commoditize.

## What would pressure the thesis

1. **Assumption:** Merchants will pay for privacy-preserving authorization rather than treat full-intent visibility as a feature.
   - **What would pressure it:** First 10 merchant conversations reveal that personalization/conversion-optimization teams *want* full agent intent and treat data minimization as a regulator-only concern with no buyer pull.
   - **Lever:** Pivot positioning from "privacy" to "fraud-and-compliance" — same SDK, but sold as agent-impersonation defense and audit evidence for high-risk verticals (corporate cards, regulated retail) where the buyer is CISO not Marketing.
2. **Assumption:** Visa, Mastercard, and Stripe will leave the predicate-privacy layer to third parties rather than absorb it.
   - **What would pressure it:** A network ships a free ZK-mandate primitive bundled with their existing token — likely at the Money2020 or FIDO Alliance roadmap level within 12 months.
   - **Lever:** Reposition above the rail-level primitive — own the cross-rail predicate library and audit ledger, where networks are structurally disincentivized to interoperate (each prefers their own walled garden).
3. **Assumption:** ZK verification can hit checkout-latency budgets at scale (<100ms p99 for a typical predicate bundle).
   - **What would pressure it:** Bundle proofs with 5+ predicates routinely exceed 200ms in real merchant tests, hurting conversion enough that merchants refuse to integrate.
   - **Lever:** Ship a "lightweight verifier" tier with cached proofs reused across merchant sessions per agent (with rotating commitments to preserve unlinkability), trading some unlinkability for latency on low-risk transactions.

## 2-week experiment

**Load-bearing assumption to test:** Mid-large merchants accepting AP2 / Stripe SPT traffic perceive an *operational* (not aspirational) need for privacy-preserving agent authorization, and would integrate a working SDK in a sandbox if shown one.

**Artifact to build (week 1):** A working `veil-demo` repo + 3-minute screencast showing:
1. A toy merchant checkout (Next.js + Stripe Checkout sandbox + AP2 mandate format).
2. An AI shopping agent (Anthropic SDK) attempting purchase with a Veil proof attached: SNARK over `{age≥18, country=DE, total≤user_cap, merchant∈agent_whitelist}` generated against a mock EUDI-style credential.
3. Merchant verifier that accepts the proof in <100ms, displays a green checkmark and a hashed attestation, completes the checkout — without ever receiving the underlying credential values.
4. A side-by-side comparison: same flow without Veil, showing the merchant database now stores the human's age, country, full intent, and credential serial.

Use existing libraries (`circom` or `noir` for the circuit, `snarkjs` for the prover, Stripe sandbox + the AP2 sample SDK from the [google-agentic-commerce GitHub](https://github.com/google-agentic-commerce/AP2)). Vincent solo with coding agents in ~5 days.

**Conversations (week 2):** 8 named, in this order: (1) 3 mid-large e-commerce platform leads (Etsy, URBN, Faire-tier), (2) 2 corporate-card platforms (Brex, Ramp product), (3) 2 Stripe / Visa partner-program contacts to test channel attractiveness, (4) 1 EU privacy regulator contact via Vincent's network for the policy read. Each conversation opens with the artifact, not a deck.

**Specific questions / asks:**
1. "Watching this checkout side-by-side — would your privacy/legal team treat the right-hand version as materially safer? What's the criterion?"
2. "If we shipped this as a Stripe-compatible add-on, what's the budget envelope and whose check would it come from?"
3. "What predicate is actually the one your team has been arguing about internally — age, jurisdiction, employer-whitelist, or something else?"
4. "What latency budget, in p99 ms, would make this a no-brainer vs. a non-starter at checkout?"
5. "If the payment networks shipped this themselves, would you still want a third-party layer for cross-rail consistency? Why or why not?"

**Pass criteria:** ≥3 design-partner LOIs (≥$25k yr 1 intent) AND ≥1 buyer puts a PO date in writing AND artifact gets ≥75 GitHub stars + ≥3 inbound from merchant CISOs / payments engineers within 14 days of public release.

**Kill criteria:** ≤1 LOI AND ≥3 of 8 conversations explicitly say "we want the full intent for personalization, not less" AND no inbound after public release. Either of (a) a payment network announces a free predicate-privacy primitive in the experiment window, or (b) Stripe/Visa privately tell us they're shipping it within 6 months — would be a hard kill.

**Vincent's effort:** ~80h total — 50h build, 30h conversations + writeup. Output: hosted demo repo + screencast + memo with quoted answers + go / pivot / kill recommendation against the criteria above.

## What we don't know yet

- What latency budget merchants actually treat as a no-go line for an extra checkout step (anecdotally <100ms p99, but unconfirmed for ZK proofs).
- Whether the right wedge is jurisdiction predicates (EU) or corporate-card predicates (B2B) — both pass the smell test, the experiment exists to differentiate.
- Whether AP2's "Verifiable Intent" co-developed with Mastercard already covers part of this and we'd be duplicating an emerging FIDO standard rather than complementing it.
- How much wallet-side adoption (EUDI rollout, World ID issuance volume) is needed before Veil's per-merchant economics are sustainable without subsidy.

## Vincent's Feedback

- Passed 2026-04-29 after walk-through.
- Consumer-privacy framing is hollow. Today's online checkout already exposes name, address, and card to the merchant — there's no real KYC happening — so the agent-mediated case doesn't introduce a categorically new privacy exposure. The proto's "merchant database now stores age, country, full intent, and credential serial" side-by-side only holds if we first assume agents push richer mandates than humans do today, which is circular: Veil exists to hide exactly the data Veil-shaped systems would put there.
- B2B procurement was the strongest residual reframe (corporate-card / employer-policy enforcement). Two beats killed it:
  - Agents are increasingly good — probably better than humans — at reading and applying a policy document. Jailbreak and prompt-injection vulnerabilities are a broader security problem the labs are working on, not a wedge for a startup. So self-enforcement of policy fit at trade time is acceptable.
  - The "independent verifier records and re-checks" role we landed on is structurally what Concur / Ramp / Brex already do today, post-hoc. Agent volume is a scaling problem for those incumbents, not a new-product opening — they own the card, the policy, and the audit ledger, so a third party slotting between them has no information asymmetry to exploit.
- Regulated-verticals carve-out (age / OFAC / license) and cross-merchant scope binding are either too featurey or already absorbed by AP2 / TAP. Not enough to anchor a company.
- Verdict: no clean third-party wedge survives. Pass on it.

## References

- [AP2 reference implementation (GitHub)](https://github.com/google-agentic-commerce/AP2) — canonical mandate format Veil's proofs must wrap; sample SDK in Python/Go/Android.
- [Cloudflare on securing agentic commerce](https://blog.cloudflare.com/secure-agentic-commerce/) — how Web Bot Auth + payment networks compose at the merchant boundary.
- [Adobe on AI-driven retail traffic surge (March 2025)](https://blog.adobe.com/en/publish/2025/03/17/adobe-analytics-traffic-to-us-retail-websites-from-generative-ai-sources-jumps-1200-percent) — ongoing evidence of the AI shopping traffic curve.
- [OWASP Top 10 for Agentic Applications 2026](https://nhimg.org/complete-guide-to-the-2026-owasp-top-10-risks-for-agentic-applications) — security framing for the buyer pitch.

## Related

- [[Whisper — ZK attestation layer for agent-to-API calls so agents prove eligibility without leaking PII]] — sibling proto on the API-side equivalent; Veil is the merchant-checkout specialization with a payment-rail co-existence story.
- [[Understanding the Math Behind ZKPs]] — Vincent's own ZK study notes informing the predicate-schema thinking.
