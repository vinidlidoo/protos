---
id: proto-veracart
aliases:
  - Veracart
tags:
  - proto
type: proto
status: drafted
created: 2026-04-28
origin: ""
proto_generator:
  seed: 396093227
  writer: 1
  writers_total: 1
  repo_sha: dc1c7d3
  generated_at: 2026-04-28T20:00:47+00:00
---

# Veracart — Cryptographic product cards that AI shopping agents can actually trust

**Wedge:** A signed, agent-readable product attestation feed for mid-market apparel brands selling into ChatGPT / Visa Intelligent Commerce / Mastercard Agent Pay — starting with the four claims agents most want to trust: price, stock, materials, and image provenance.

## What is it?

Veracart is a thin SaaS layer that sits between a brand's PIM/commerce stack and the new agent surfaces (ChatGPT Instant Checkout, Salesforce Agentforce Commerce, the Visa/Mastercard agent rails). It publishes each SKU's commerce-critical claims — price, stock, materials, country-of-origin, certifications, and the C2PA provenance of every product photo — as a cryptographically signed "Verified Product Card." The card is delivered through the brand's existing agent feed (the Shopify [Agentic Commerce app](https://shopify.dev/docs/agents), Salesforce's [Agentforce feed](https://www.salesforce.com/commerce/ai/agentic-commerce/), or a standalone JSON endpoint) and verified at agent-side before the agent recommends or buys.

The brand pays Veracart to make their catalog *machine-trustworthy*: when a buyer's agent compares two indistinguishable wool sweaters, the one with a verified "100% merino, mulesing-free, photographed unedited in Lisbon on 2026-03-12" attestation wins the cart. The agent doesn't need to trust the brand — it verifies the signature. Brands get a measurable lift in agent-driven conversion plus a head start on the EU Digital Product Passport regulation.

## Why now (2026)

- Adobe Analytics measured generative-AI referral traffic to US retail sites up **~693%** during the 2025 holiday season YoY — the agent-driven channel is now a real growth vector that brands must be discoverable and trustworthy on ([Adobe](https://news.adobe.com/news/2026/01/adobe-holiday-shopping-season)). Visa expects "millions of consumers" using shopping agents by the 2026 holiday season ([Visa](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.21961.html)).
- Stripe + OpenAI's [Agentic Commerce Protocol](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol) shipped to production September 2025 and powers Etsy + Shopify Instant Checkout in ChatGPT ([Stripe](https://stripe.com/blog/developing-an-open-standard-for-agentic-commerce)). PayPal and Mastercard moved to support ACP-style flows in late 2025 ([Payments Dive](https://www.paymentsdive.com/news/paypal-mastercard-partner-agentic-strategy/803869/)). The *transport* is settled; the **claims layer** on top of it is wide open.
- Visa shipped the [Trusted Agent Protocol](https://github.com/visa/trusted-agent-protocol) and Mastercard shipped [Verifiable Intent](https://www.mastercard.com/us/en/news-and-trends/stories/2026/verifiable-intent.html) to verify *the agent's identity to the merchant*. Nobody has shipped the symmetric thing: verifying *the merchant's product claims to the agent*.
- C2PA crossed **6,000+ members and affiliates** by January 2026, with Google embedding Content Credentials directly into Pixel 10 and Sony among the camera adopters — content provenance is becoming a default expectation in media, and product imagery is the obvious next surface ([C2PA state-of-the-union 2026](https://contentauthenticity.org/blog/the-state-of-content-authenticity-in-2026)).
- The EU Ecodesign for Sustainable Products Regulation sets a textile-DPP delegated act for **2027**, with mandatory compliance for apparel sold in the EU realistically arriving **mid-2028** (~18 months after adoption) ([Carbonfact / DPP for fashion](https://www.carbonfact.com/blog/policy/digital-product-passport-fashion), [JRC textile DPP study](https://www.europarl.europa.eu/RegData/etudes/STUD/2024/757808/EPRS_STU(2024)757808_EN.pdf)). Brands need a place to publish signed claims regardless — the agent surface is the natural early-adopter wedge that earns ROI before the regulatory deadline bites.
- Zero-knowledge extensions to DPPs (proving "≥50% recycled content" without revealing supplier data) are now an active research / standards thread, removing the last brand objection — "we can't expose our supply chain" ([Preprints / ZK-DPP, Dec 2025](https://www.preprints.org/manuscript/202512.1689)).

## Who else is doing this

- **Agent-identity rails (the symmetric problem)** — main player: **[Visa Trusted Agent Protocol](https://developer.visa.com/use-cases/trusted-agent-protocol)** + **[Cloudflare Web Bot Auth](https://blog.cloudflare.com/web-bot-auth/)**. Others: [Mastercard Verifiable Intent](https://www.mastercard.com/us/en/news-and-trends/stories/2026/verifiable-intent.html), [World ID AgentKit](https://techcrunch.com/2026/03/17/world-launches-tool-to-verify-humans-behind-ai-shopping-agents/). They prove *who the agent is and that a real human is behind it* — the inverse of our problem. Complementary, not competing.
- **Agent-readable product feeds (plumbing, no verification)** — main player: **[Shopify Agentic Commerce](https://shopify.dev/docs/agents)**. Others: [Salesforce Agentforce Commerce](https://www.salesforce.com/commerce/ai/agentic-commerce/), [Feedoptimise SFCC agent](https://www.feedoptimise.com/integrations/sources/salesforce), [agenticcommerce.cloud](https://agenticcommerce.cloud/shopify). They deliver the data; nothing in any of these stacks signs the claims. A merchant can put any number in any field.
- **Digital Product Passport vendors (regulatory plumbing, not agent-facing)** — main players: **[Circularise](https://www.circularise.com/blogs/digital-product-passports-dpp-what-how-and-why)**, [TrusTrace](https://trustrace.com/knowledge-hub/how-fashion-brands-can-prepare-for-the-eu-digital-product-passport-a-practical-guide-1), [Carbonfact](https://www.carbonfact.com/blog/policy/digital-product-passport-fashion), [Avelero](https://www.avelero.com/updates/fashion-digital-product-passport-timeline/), [Spherity](https://medium.com/spherity/implementing-digital-product-passports-using-decentralized-identity-standards-f1102c452020). Selling DPP compliance to apparel brands. Treat the QR-code-on-a-hangtag as the deliverable. None expose a real-time, agent-queryable verification endpoint.
- **Image provenance (single-claim point solutions)** — **[Adobe Content Credentials / CAI](https://contentauthenticity.org/how-it-works)**, [Truepic](https://truepic.com/), [Numbers Protocol](https://numbersprotocol.io/). Sign images at capture. Solve provenance for one field; nobody bundles it with price/stock/materials into a single agent-verifiable card.

**Structural gaps:** The payment networks own *agent identity* and won't naturally extend into *product claims* (regulatory/scope risk for them). The DPP vendors own *regulatory compliance* and ship it as a static QR code, not as a live signed feed. The commerce platforms (Shopify, Salesforce) own the agent feed pipe but can't credibly sign their merchants' claims (conflict of interest — they earn take-rate on every sale, including the dishonest ones). The opening is a neutral, vertical-focused **claims-layer specialist** that bundles existing primitives (C2PA + DID/VC + ZK extensions + ACP) into one product an apparel CMO actually understands.

## Why us

- **Cryptography depth + e-commerce category gut is rare.** Vincent shipped a multi-part zk write-up while running a 5-year stint as chief-of-staff / category / PM in Amazon Fashion. The DPP/C2PA founders are crypto-native and don't speak "lifestyle imagery, A+ content, return rates"; the apparel-tech founders don't speak "verifiable credentials, signed manifests, ZK range proofs." This bet sits on the seam.
- **Trilingual EN/FR/JA + Seattle base** maps to the three regions where this becomes mandatory or commercially urgent first: EU (regulation), US (Stripe/OpenAI/Visa rails), Japan (high counterfeit-sensitivity, premium apparel exports). Most claims-layer competitors will be EU-only or US-only.

## Customer & buyer

- **Customer:** Head of Digital / Head of Ecommerce at a $50M–$500M GMV apparel brand selling DTC + wholesale, with active EU revenue.
- **Buyer:** Same person, or VP Commerce. Budget line is "agentic commerce enablement" or "EU compliance" depending on which urgency lands first. Typical ACV target: $30K–$80K year-1.
- **Champion:** Often the in-house data/PIM lead, who already owns the product feed mess and is being asked to "make us work in ChatGPT."
- **ICP test:** EU revenue ≥10% of total, ≥5,000 active SKUs, already has a PIM (Akeneo / Salsify / Plytix), already publishing to Shopify Agentic Commerce or Salesforce Agentforce, *and* has at least one product line where authenticity / sustainability / provenance is part of the brand promise (premium denim, wool, leather, technical outdoor).
- **Anti-customer:** Pure-fast-fashion brands with no provenance story (the claims would expose them) and DTC-only US brands with zero EU exposure (no regulatory urgency, agent-volume case alone won't carry an enterprise sale yet in 2026).

## Wedge / where we could enter

- **Candidate A — Premium wool / merino apparel.** Tight regulatory pressure (Australia mulesing disclosure + EU DPP), high counterfeit/greenwashing damage, photogenic provenance story. ~50 brands globally meet the ICP. Could ship a working "verified merino card" as a demo with one brand and use it as the wedge case-study.
- **Candidate B — Premium denim.** Indigo/cotton sourcing claims, high return rates that better claims could reduce, EU-heavy customer base. Slightly less regulatory urgency than wool but bigger TAM.
- **Candidate C — Japanese premium apparel exporting to EU/US.** Vincent's Japanese-language access + Japan's authenticity-fetish culture make this an unusual angle competitors can't reach. Smaller brands but higher willingness to pay per SKU.

What would push us toward one: where the first 3 design-partner LOIs land in the experiment. If Japanese inbound interest is high, lean Candidate C; if a single brand will commit to a public case study, lean A.

## What makes it defensible

- **(a) Primary — Two-sided trust graph.** Every signed claim accumulates a verification log: agents that consumed it, transactions that closed against it, disputes that did or didn't fire. Over time Veracart becomes the *source of truth on which claims actually drive conversion in agent contexts*. New entrants ship signing infra; we ship signing infra + the only outcome data set. This compounds with every agent transaction we sit between.
- **(b) Secondary — Agent-side trust list integrations.** Once ChatGPT Shopping, Perplexity Comet, and the Visa/Mastercard agent SDKs accept Veracart-signed claims as "high-trust" inputs, switching costs for brands rise sharply. The work to get on those lists is slow, relationship-heavy, and protocol-fluent — exactly what a generalist competitor can't shortcut.
- **(c) Year-3 endgame — Become the issuer-of-record for EU DPP fashion data.** When the textile delegated act lands (~2027) we're already the cryptographic backbone for several lighthouse brands; we extend the same signed-claim infrastructure to satisfy the regulatory reporting endpoint. Veracart-signed claims become both the agent-trust signal and the regulatory artifact, in one feed.

## How it could make money

| Layer                                                                              | Price range                                          | Comparable (public pricing where available)                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Layer 1 — Verified Card SaaS (per-brand subscription)**                          | $30K–$80K / yr                                       | [Akeneo PIM Growth Edition starts at ~$25K/yr](https://www.g2.com/products/akeneo-pim/pricing) (low-end anchor — adjacent catalog SaaS); [Salsify per Sitation](https://www.sitation.com/topic/salsify/pricing/): "around $2,000–$5,000 per month" for smaller customers (~$24K–$60K/yr), "significantly more" for larger enterprise — closest PIM peer, brackets the $30K–$80K range from the small-customer band into the enterprise tier |
| **Layer 2 — Per-attestation usage fee (image provenance, ZK supply-chain proofs)** | $0.05–$2.00 per signed claim (depending on richness) | [Truepic Vision Growth Plan](https://www.truepic.com/pricing): $1,450/mo ($17,400/yr) headline, $58/inspection list price, overages billed $28–$65/inspection by tier; Enterprise = custom. Truepic includes human-witnessed inspection — sets the *ceiling*. Veracart's automated signed-claim layer should price 1–2 orders of magnitude below                                                                                            |
| **Layer 3 (later) — % of agent-driven GMV**                                        | 0.5%–1.5% of agent-driven GMV                        | [Salesforce Commerce Cloud's GMV-share model](https://twelverays.agency/blog/salesforce-commerce-cloud-pricing): 1%/2%/3% of GMV across B2C Starter/Growth/Plus tiers — directly brackets and validates the GMV-share monetization shape for catalog-adjacent SaaS                                                                                                                                                                          |

Honest caveats: (a) Layer 2's per-attestation rate has no perfect comparable — Truepic's pricing reflects human-witnessed inspections, which is a richer (and more expensive) product than what Veracart would sell; the experiment must price-discover the actual willingness to pay for automated signed claims. (b) Layer 1 alone (at the $30K–$80K ACV range) is plausible as the wedge but may not clear the bar for venture-scale; if Layer 2 or Layer 3 don't open up, this drifts toward a great $5–10M ARR services-flavored business rather than a $100M one. (c) Layer 3 puts us in revenue-share territory adjacent to Stripe/Visa take-rates — careful positioning required to avoid collision.

## What would pressure the thesis

1. **Assumption:** Apparel agents will materially differentiate between "signed" and "unsigned" claims when ranking products in the next 18 months.
   - **What would pressure it:** ChatGPT Shopping, Perplexity, and Salesforce Agentforce all stay agnostic to provenance signals through 2027 and rank purely on price + reviews + brand authority.
   - **Lever:** Pivot priority customer from "brands wanting agent lift" to "brands wanting EU DPP compliance," lean on the regulatory clock and let the agent-trust angle accrue passively.
2. **Assumption:** Stripe + Visa + Mastercard will *not* extend their agent-commerce stacks into product-claim attestation themselves.
   - **What would pressure it:** Stripe ships a "Verified Product" extension to ACP; Visa expands Trusted Agent Protocol scope to include merchant-side product attestations.
   - **Lever:** Become the reference vertical implementation — partner rather than compete. Be the apparel-specific opinionated layer on top of their generic primitives. Worst case acquisition target.
3. **Assumption (potentially the killer):** Apparel brands' legal teams will allow them to cryptographically sign product claims with cryptographic non-repudiation — i.e. accept the liability exposure that comes with a signature they can't later disavow.
   - **What would pressure it:** First three legal-review conversations come back with "we will never sign a claim about our supply chain." If this is universal, the entire signed-claims model collapses regardless of demand or tech maturity.
   - **Lever (defensive):** Restrict the v1 attestation surface to claims the brand already self-warrants on the PDP itself (price, stock, photo provenance, country-of-origin from the customs manifest) — these have *zero* incremental legal risk over what's already on the website. Treat material composition and sustainability claims as a Year-2 upsell once the legal pattern is established. Lever (offensive): partner with a third-party auditor (Carbonfact, TrusTrace) so the *auditor* signs the substantive claims and the brand only signs that the audit is current — shifting liability off the brand entirely.
4. **Assumption:** The EU DPP textile timeline holds (delegated act late 2026 / early 2027, mandatory ~2028).
   - **What would pressure it:** Slippage to 2030+, removing the regulatory tailwind.
   - **Lever:** Lean harder on the agent-conversion ROI story; cut sales motion length by emphasizing agent-traffic case studies over compliance.

## 2-week experiment

**Load-bearing assumption to test:** That a Head of Ecommerce at a premium apparel brand will, after seeing a working signed-card demo running against their own SKUs, commit to a paid pilot — and that at least one buy-side surface (an agent dev, a commerce platform PM) confirms they'd boost Veracart-signed listings.

**Artifact to build (week 1):** A live, public **"Verified Card" demo site** at veracart.dev (or similar) that:

1. Takes a real public PDP URL from 5 named premium-apparel brands (one each: Allbirds, Patagonia, Pangaia, Naadam, Iris von Arnim — chosen for varied provenance stories).
2. Generates a signed Verified Product Card for each: price + stock pulled live from their public APIs/scrapes; image provenance computed from C2PA manifests where present and flagged "unverified" where not; materials and country-of-origin pulled from PDP copy and *flagged as brand-asserted vs. independently verified*.
3. Includes a side-by-side widget where a visitor can paste any apparel PDP URL and get a signed card back in <10 seconds.
4. Includes a "consume from an agent" demo: a hosted ChatGPT custom GPT or a small CLI that fetches the card, verifies the signature, and rejects/accepts based on policy. This is the load-bearing piece — it shows the *consumption* side, not just the issuance.

Built solo by Vincent in ~5 working days using coding agents. Stack: Cloudflare Workers + Web Bot Auth, [c2pa-rs](https://github.com/contentauth/c2pa-rs) for image provenance, a tiny issuer service, a public JSON-LD VC schema. Hosted; publicly linkable.

**Conversations (week 2):** 12 calls, all opened by sharing the live demo URL 24 hours before:

- 6 with Heads of Ecommerce / Digital at $50M–$500M apparel brands (warm intros via Vincent's Amazon Fashion network + cold outreach to brands listed in the demo).
- 3 with PMs at agent surfaces: Shopify Agentic Commerce, Salesforce Agentforce, one of Perplexity / OpenAI shopping.
- 2 with EU DPP solution architects (Carbonfact, TrusTrace, or similar) to test acquisition / partnership angle.
- 1 with a Visa or Mastercard agent-commerce product person, to confirm we're not on a collision course.

**Specific questions / asks (each answerable in 30 min while looking at the demo):**

1. "If this card existed for your top 100 SKUs, would you pay $X/month for it? At what X does it become an instant yes?"
2. "Which of the four signed claims (price, stock, materials, image provenance) would you ship first? Which are you not legally comfortable signing today, and why?"
3. "On the agent side: would your platform treat a Veracart-signed listing differently than an unsigned one in ranking? What would have to be true for you to publicly say so?"
4. "Where does this die inside your org — legal, IT, the brand team, or procurement?"

**Pass criteria:** ≥3 brand LOIs for paid pilots **AND** ≥1 agent-surface PM willing to do a public co-marketing test **AND** demo gets ≥150 GitHub stars / ≥5 inbound emails from brands not on the contacted list.

**Kill criteria:** <2 LOIs, **OR** every brand says "this is a CMO conversation, not a Head of Ecommerce one" (signals 18+ month sales cycle = wrong wedge), **OR** an agent-side PM tells us a payment network has already announced this exact product internally.

**Vincent's effort:** ~80 hours total. Split: 40 hrs build (week 1, mostly coding-agent supervised), 30 hrs conversations (week 2, ~2.5 hrs/call including prep), 10 hrs writing the memo with quoted answers + go/pivot/kill recommendation. Output: hosted demo + public GitHub repo + memo.

## What we don't know yet

- How quickly ChatGPT Shopping / Perplexity / Comet will actually expose a "trusted feeds" allowlist that we could get into — could be 6 months, could be 24.
- Whether the DPP delegated act for textiles will end up mandating a specific signature scheme that locks out our chosen primitives (need to read the late-2026 draft when it lands).
- Whether the right wedge persona is brand-side (Head of Ecommerce) or agent-side (an AI shopping agent that wants to differentiate by being the "trustworthy" one). The experiment tests brand-side first because it's where the money is, but agent-side could be a faster path.
- Whether ZK-of-supply-chain proofs are mature enough today to ship for premium-cotton or merino claims, or whether we punt and start with C2PA + plain signed claims.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Stripe — Developing an open standard for agentic commerce](https://stripe.com/blog/developing-an-open-standard-for-agentic-commerce) — context on ACP's adoption curve and what the protocol does/doesn't standardize.
- [Cloudflare — Securing agentic commerce with Visa and Mastercard](https://blog.cloudflare.com/secure-agentic-commerce/) — clearest single piece on how the agent-identity layer is being assembled.
- [EU JRC study on textile DPP](https://www.europarl.europa.eu/RegData/etudes/STUD/2024/757808/EPRS_STU(2024)757808_EN.pdf) — authoritative timeline for the textile DPP delegated act.
- [Preprints — ZK extensions for DPPs](https://www.preprints.org/manuscript/202512.1689) — the academic substrate for the privacy-preserving claims piece.
- [PYMNTS — Know Your Human in agentic commerce](https://www.pymnts.com/artificial-intelligence-2/2026/agentic-commerce-pushes-know-your-human-into-verification-processes/) — frames the inverse problem (we're solving "Know Your Product" for agents).

## Related

- [[Study/Aave Deep-Dive]]
- [[Templates/proto]]
