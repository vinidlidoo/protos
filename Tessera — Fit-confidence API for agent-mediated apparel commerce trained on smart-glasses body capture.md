---
id: proto-tessera
aliases:
  - Tessera
tags:
  - proto
type: proto
status: passed
created: 2026-04-28
origin: ""
proto_generator:
  seed: 857077097
  writer: 1
  writers_total: 1
  repo_sha: b29aa01
  generated_at: 2026-04-29T01:50:34+00:00
---

# Tessera — Fit-confidence API for agent-mediated apparel commerce, trained on smart-glasses body capture

## What is it?

**Elevator pitch**: Tessera sells apparel retailers (and the shopping agents who buy on behalf of consumers) a single API call — `POST /fit-confidence` with a SKU + a shopper ID — that returns a calibrated probability the garment will be kept, plus the size most likely to fit. The shopper's body model is built once from a 30-second smart-glasses capture (mirror walk-around) and re-used across every brand. Retailers cut size-driven returns; shopping agents stop guessing and start buying with conviction.

**How it works**: A consumer with Ray-Ban Meta or similar glasses runs a one-time guided capture in front of a mirror; we extract ~80 measurements + body-shape embedding via on-device vision, then store a privacy-preserving body vector keyed to a Tessera ID. Brands ingest their existing tech-pack measurements + return-reason data via a feed. At query time, our model combines the body vector, the garment's geometry, the brand's historical fit drift, and (where available) returned-garment signals to emit a calibrated keep-probability per size. Agents (OpenAI Operator, Perplexity, ChatGPT shopping) call the API before placing an order; retailers call it on the PDP and inside agentic checkout flows.

## What's the problem?

Online apparel returns hit ~24.4% in the US, a roughly $38B/yr drag, and **53% of those returns are size/fit-driven** ([Coresight](https://coresight.com/research/the-true-cost-of-apparel-returns-alarming-return-rates-require-loss-minimization-solutions/)). Today retailers patch the leak with size-recommender widgets that infer fit from declared height/weight + purchase history — useful, but ground-truth-blind. Meanwhile, shopping agents (ChatGPT Instant Checkout, Operator, Perplexity Shopping) are starting to place real apparel orders for users who never see the PDP — and they have *no structured fit signal at all*. The default fallback is the bracketing behavior — buying multiple sizes intending to return what doesn't fit — that consumers openly admit to ([upcounting on the bracketing pattern](https://www.upcounting.com/blog/average-ecommerce-return-rate)) and that keeps clothing returns parked in the high twenties.

## Why now (2026)

- **Smart-glasses install base just crossed the threshold where mirror capture is realistic.** EssilorLuxottica + Meta sold 7M+ AI glasses in 2025 alone — more than triple all prior years combined ([UploadVR on EssilorLuxottica earnings](https://www.uploadvr.com/meta-essilorluxottica-sold-7-million-smart-glasses-in-2025/)) — and Meta launched prescription Gen-2s at $499 in March 2026 ([Meta Newsroom](https://about.fb.com/news/2026/03/meta-ai-glasses-built-for-prescriptions/)). Camera-first wearables on millions of faces is what makes a one-time body capture a consumer-tolerable action rather than a niche kiosk visit.
- **Agentic apparel checkout went from demo to live infra in the last 12 months.** Stripe + OpenAI launched the Agentic Commerce Protocol and ChatGPT Instant Checkout on Sept 29, 2025 ([Stripe newsroom](https://stripe.com/newsroom/news/stripe-openai-instant-checkout)); Salesforce's pilot now syndicates Crocs and Pacsun product data into ChatGPT discovery, with Pacsun explicitly using it to reach Gen Z/Gen Alpha shoppers ([Salesforce/OpenAI pilot coverage](https://www.digitalcommerce360.com/2026/04/13/salesforce-pilot-integration-openai-chatgpt/)). Apparel is in the first wave, not a hypothetical 2028 expansion.
- **Morgan Stanley's AlphaWise has US LLM adoption near 50% with agents already on track for 10-20% of e-commerce ($190-385B)**, and McKinsey projects $900B-$1T in US agentic-commerce GMV by 2030 ([Opascope citing Morgan Stanley + McKinsey](https://opascope.com/insights/ai-shopping-assistant-guide-2026-agentic-commerce-protocols/)). Once an agent is doing the buying, fit-confidence becomes a per-call decision input — not a UI widget.
- **EMG + display unlocks make the 30-second capture flow feel native, not awkward.** Meta Ray-Ban Display + Neural Band ($799, Sept 2025) means the user can be coached through a mirror walk-around with on-lens visual prompts and pinch-confirmations — no phone, no app open ([Meta Connect 2025](https://about.fb.com/news/2025/09/meta-ray-ban-display-ai-glasses-emg-wristband/)).
- **Egocentric body-vision research is now production-ready.** Meta's Project Aria Research Kit applications are open for Gen 2 hardware, and the public Aria Gen 2 Pilot and Aria Digital Twin datasets give a credible foundation for body-pose + measurement models built from glasses-POV video ([Project Aria](https://www.projectaria.com/)). The model science isn't speculative; the productization is.
- **Returns economics keep getting worse.** Coresight: it costs ~66% of a product's price to process a return; 67% of brands say zeroing returns would lift bottom-line by 20%+ ([Coresight](https://coresight.com/research/the-true-cost-of-apparel-returns-alarming-return-rates-require-loss-minimization-solutions/)). Buyers feel the pain monthly.

## Who else is doing this

- **Incumbent purchase-history fit engines** — main player: **[True Fit](https://www.truefit.com/)**. Others: [Fit Analytics](https://fitanalytics.com/) ([Snap-acquired in 2021](https://techcrunch.com/2021/03/17/snap-is-taking-a-significant-step-into-fashion-e-commerce-with-its-acquisition-of-fit-analytics/)), [Fitezapp](https://www.fitezapp.com/blog/reduce-fashion-returns.html). They infer fit from declared sizes + 80M+ shoppers' purchase/return behavior. Strong on aggregate calibration, blind on individual ground-truth body. True Fit recently shipped an "MCP integration for AI labs" — they see the agent surface coming, but their data spine is still purchase-event inference.
- **Mobile-camera body-scan players** — main player: **[3DLook](https://3dlook.ai/)**. Others: **[Bodidata](https://www.bodidata.com/blog/the-search-engine-for-apparel-fit)** (radar-based 3D body scanner, fully-clothed). 3DLook gets ~80 measurements from 2 phone photos. Closest to our data layer, but their distribution model is a per-retailer SDK in the consumer purchase flow — friction at exactly the point we'd skip by capturing once via glasses ambient.
- **Smart-glasses platform owners themselves** — **[Meta Ray-Ban](https://www.meta.com/ai-glasses/ray-ban-meta/)**, **[Snap Spectacles](https://www.spectacles.com/)**, Apple/Google. They own the camera but their incentive is to keep body-derived data on-device or as platform property; they will not ship a multi-brand fit-confidence API. They're a distribution channel, not a competitor for the API tier.
- **Generative virtual try-on** — **[Google Doppl](https://blog.google/technology/google-labs/doppl/)**, retailer-built try-on widgets. Visual confidence ≠ fit confidence; they answer "how does it look on me" not "will I keep my standard size in this brand." Complementary, not substitutive.

**Where the opening is.** True Fit owns purchase-history inference. 3DLook owns mobile-camera capture. Meta owns the glasses. None of them is building the *agent-callable, brand-portable, body-truth-grounded* fit API. True Fit can't pivot to body-truth without abandoning their data moat; 3DLook can't pivot to ambient capture without abandoning their checkout-time SDK; Meta won't open the body-data primitive because it commoditizes their platform. The wedge is a neutral fit layer that treats the glasses as a sensor and the agent as the buyer — the role neither the incumbent nor the platform wants to play.

## Why us

- **Vincent did 5 years inside Amazon Fashion in chief-of-staff and category/PM roles** — he has direct line of sight to which retail buyer (returns ops? merchandising? agentic-commerce lead?) actually has the budget and the pain, and what dashboard their reviews actually open with. That collapses the discovery loop that kills most B2B retail-tech startups in year one.

## Customer & buyer

- **Customer**: The agentic-commerce / digital lead at a mid-to-large apparel brand or marketplace ($200M–$5B GMV). Also: shopping-agent platform PMs at OpenAI/Perplexity/Anthropic who need a fit signal in their tool registry.
- **Buyer**: VP of E-commerce or Chief Digital Officer (return-rate is on their P&L line). Budget line: returns-reduction tooling, typically pulled from logistics-loss budget, $300K–$2M ACV at the top end.
- **Champion**: The merchandising-ops director or returns-ops manager who is tired of fielding the quarterly "why is our return rate 28%" question.
- **ICP test**: ≥$500M apparel GMV; current size-driven return rate ≥18%; already piloting at least one shopping-agent integration (ACP, Shopify Magic, Perplexity merchant) OR has an internal AI-shopping initiative on the 2026 roadmap.
- **Anti-customer**: Long-tail Shopify boutiques (no integration capacity, low absolute return-cost), pure luxury (low return rate, high-touch styling already), made-to-measure (different problem entirely).

## Wedge / where we could enter

- **Candidate A — Returns-reduction pilot with one mid-large apparel retailer.** Tessera ships a per-SKU fit-confidence widget to the PDP for users who opt in via glasses capture. We get measured against their existing recommender on size-driven return delta. Direct, concrete, but agent-blind.
- **Candidate B — "Fit signal in the agent tool registry."** We become a tool/skill that ChatGPT/Operator/Perplexity shopping agents call before placing an apparel order. Wider distribution, but we depend on agent platforms surfacing us — and on consumers having captured.
- **Candidate C — Direct-to-glasses-platform partnership** (Meta or Snap) where the capture flow is built into the OS-level "fit" assistant and we license the recommendation engine. Fastest distribution, but commoditization risk: Meta could build it themselves once the data flywheel is proven.

What pushes us toward A: a real return-rate delta is the most defensible reference customer. It buys us standing for both B and C. **A is the lead candidate**, with B as the parallel narrative that makes the bet 5-year-interesting.

## What makes it defensible

- **(a) Primary — the body-vector data network.** Each shopper captures once and reuses across every brand on Tessera. Each brand contributes returned-garment signal that calibrates fit drift on every other brand's catalog. Two-sided flywheel: more shoppers makes Tessera more useful per brand; more brands makes capture more valuable per shopper. Compounds with both.
- **(b) Secondary — agent-tool registry placement.** First-mover into shopping-agent tool registries (ACP, Anthropic MCP, Perplexity) is sticky: agents cache tool selections, and the cost of swapping a fit-confidence provider mid-stack is non-trivial once it's wired into checkout.
- **(c) Year-3 endgame — the fit-truth dataset.** A privacy-preserving corpus mapping body-vector → garment-geometry → keep/return outcomes is uniquely valuable to brand designers (sizing curve correction), to platform owners (Meta/Apple wanting native fit features), and as defensive moat (incumbents can buy access but not replicate the longitudinal capture flow).

## How it could make money

| Layer                        | Price range                              | Comparable                                                          |
| ---------------------------- | ---------------------------------------- | ------------------------------------------------------------------- |
| **Per-API-call fit query**   | $0.01–$0.05 per call                     | [Anthropic web-search tool: $10 per 1,000 searches](https://platform.claude.com/docs/en/about-claude/pricing) (adjacent agent-stack per-call pricing precedent) |
| **Brand SaaS subscription**  | $80K–$500K/yr per brand (tiered by GMV)  | [True Fit](https://www.truefit.com/) (private; comparable bracket)  |
| **Year-3: Sizing-curve data licensing to brand designers** | $250K–$1M/yr per brand | [3DLook Body Data Licensing](https://3dlook.ai/)                    |

**Honest caveat**: Layer 1 is a chicken-and-egg market — agent-mediated apparel volume is real but small in 2026, and per-call pricing only works once it scales. Layer 2 (brand SaaS) is where year-1 revenue lives, and it competes directly with True Fit's installed base — so the pitch must be "ground-truth body, not declared sizes" or we lose on inertia. Layer 3 only materializes if the data flywheel actually spins; if capture adoption stalls, Tessera is just another size-recommender vendor.

## What would pressure the thesis

1. **Assumption**: Consumers will tolerate a 30-second mirror body-capture flow to unlock cross-brand fit accuracy.
   - **What would pressure it**: ≤15% completion rate among glasses owners offered the capture in a controlled flow, OR strong privacy backlash post-launch (e.g., a media cycle around "Meta-glasses body-scan tracking").
   - **Lever**: Shift to passive ambient inference from glasses-POV mirror reflections (no explicit ask), at the cost of accuracy and a longer model dev runway.
2. **Assumption**: At least one large brand will pay a premium for body-truth-grounded fit prediction over True Fit's purchase-inference baseline.
   - **What would pressure it**: A pilot where Tessera's size-driven return delta vs True Fit is ≤3pp — within margin-of-noise for the buyer's CFO.
   - **Lever**: Reposition as the agent-distribution layer (Candidate B) and let True Fit own the brand-PDP layer; we tax agent calls instead.
3. **Assumption**: Shopping agents will become a meaningful fraction of apparel GMV by 2028 (≥10%).
   - **What would pressure it**: Agentic commerce stalls or fragments into walled gardens (Amazon won't let agents buy on its catalog; Shopify's agent stays Shopify-only). Layer 1 evaporates.
   - **Lever**: Lean entirely on Layer 2 (brand SaaS) and Layer 3 (data licensing); accept slower growth path.
4. **Assumption**: Meta/Apple won't ship a native, free, glasses-OS-level fit feature within 24 months of our launch.
   - **What would pressure it**: Meta announces a "Ray-Ban Fit" or Apple a "Vision Fit" SDK at WWDC/Connect.
   - **Lever**: Pivot to multi-brand neutrality and brand-data-aggregation as the pitch; the platform owners cannot credibly be neutral to brand catalogs they don't own.

## 2-week experiment

**Load-bearing assumption to test**: A retail VP/CDO will pay (or sign an LOI) for a fit-confidence signal *if* we can show a credible body-truth pipeline that beats their current size-recommender on a small set of real garments.

**Artifact to build (week 1)**: A working browser demo where Vincent (filmed via webcam-as-glasses-proxy doing a guided 30-sec mirror walk-around) gets back ~60 body measurements + size predictions for 5 real apparel SKUs across 3 brands (Uniqlo, Levi's, Patagonia — chosen for public fit-spec PDFs). The demo:
1. Runs a public off-the-shelf body-pose model (e.g., MediaPipe + a 3D-fit head) on the capture.
2. Cross-references the brand's published fit-spec table.
3. Returns a calibrated keep-probability per size, with confidence band visible.
4. Includes a side-by-side "True Fit baseline" using only declared height/weight, so the gap is visceral.
Hosted at tessera.fit, screencast embedded, plus a short Loom walkthrough that opens with "buyer, here's what your CDO sees on Tuesday."

**Conversations (week 2)**: 6 named buyer conversations, each opening with the artifact open in their browser:
- 3 VP-of-Ecom or CDO at apparel brands $500M–$3B GMV (Vincent's Amazon Fashion network — warm intros)
- 2 PMs working on shopping-agent product (OpenAI ACP team, Perplexity Shopping, or equivalent)
- 1 incumbent (True Fit, 3DLook) for landscape-truthing — *not* a sales call, an honest "is this the right wedge" probe

**Specific questions / asks (asked while artifact is on screen)**:
1. "If this returned a >0.85 keep-probability for size M and your buyer accepted that as the recommendation, what would you need to see to greenlight a 90-day pilot?"
2. "Where does this signal need to live for you — PDP widget, agent tool, returns dashboard, all three?"
3. "What's the smallest pilot you'd write a PO for? Per-API-call, flat fee, gainshare on returns delta?"
4. "If we got this in front of your shopping-agent integrations team next month, who do we need in the room?"

**Pass criteria**:
- ≥3 LOIs or signed pilot intent from $500M+ GMV apparel buyers
- ≥1 buyer naming a concrete PO date in 2026
- Artifact gets ≥1 inbound from someone we didn't approach (X share, agent-platform PM, investor)
- ≥1 of the 2 agent-platform PMs says "send us the API spec, we'll look at registry inclusion"

**Kill criteria**:
- 0 of 3 brand-side conversations open with "this is solving the right problem" — they'd push back on returns-as-priority or on body-capture as feasible
- The body-pose pipeline accuracy is so visibly bad on the demo that buyers don't believe a real version would be better
- Both agent-platform PMs say "fit-confidence is a per-merchant problem, not a registry-tool problem"

**Vincent's effort**: ~70 hours total. ~45h build (4 days, coding-agent-led: pose pipeline + brand fit-spec ingest + calibrated probability head + minimal UI), ~15h conversations + scheduling, ~10h memo + recommendation. Output: tessera.fit live demo, screencast, memo with quoted answers, go/pivot/kill recommendation.

## What we don't know yet

- What body-capture flow actually clears the consumer-tolerance bar — passive (ambient mirror inference) vs guided (30-sec walk-around) vs progressive (capture during a real "trying clothes on" moment).
- Whether brand-side or agent-side distribution is the faster wedge in practice — A vs B in section above is a real coin-flip until we run pilot conversations.
- Privacy / regulatory exposure of storing body vectors. GDPR Article 9 (biometric data) is a real question; the right answer may be on-device-only inference with a thin server-side embedding, but we haven't legal-checked.
- Whether True Fit's MCP integration is real production traffic or a press-release move — affects how aggressively they'd defend the agent-tool registry slot.

## Vincent's Feedback

**Decision: kill.** Not because the idea is bad — surprisingly insightful actually — but because I worked the fit problem for 2-3 years inside Amazon Fashion (2016-2018) and I'm tired of the space. Success probability here is too low relative to my motivation to work on it. Recording the technical reasoning anyway in case the wardrobe-scan unlock below becomes relevant in another shape.

**What's right about the proto.** Two convergent unlocks: (a) smart glasses make body capture tolerable in a way phones never did — the awkwardness was the bottleneck, not the model science; (b) agent-mediated apparel commerce creates a real need for a structured fit signal that doesn't exist today. Both bets are correct.

**The hole the proto doesn't close — data acquisition.** Body measurements + tech-pack dimensions tell you the garment's geometry, not whether a body shape will *like* the cut/ease/drape in a specific brand. The label space is body-vector × SKU × kept/returned/why, and that data is brand-proprietary. Amazon especially will not share — they treat it as a strategic asset and were building this internally when I was there. True Fit's 15-year moat is exactly that they got embedded in checkout flows and traded the widget for return-reason access. A startup has none of that.

**The clever unlock the proto misses — wardrobe scan + reverse fit inference.** Use glasses (or even a phone) at home: scan the clothes already in your wardrobe that fit well, identify each garment's SKU and size from the label, look up the brand's published tech-pack, and back out the user's *preferred-fit envelope* per garment type. From there, recommend other brands' SKUs that match the same envelope. This sidesteps the data-acquisition problem entirely — no brand needs to share return data, because the user's wardrobe *is* the labeled training set ("I kept these, they fit me, here are their dimensions"). Doesn't need agent-checkout integration to start; works as a standalone consumer app.

**Why this still isn't a big enough business for me.** The wardrobe-scan unlock is executable by anyone with an existing fashion retail business — Amazon could ship it tomorrow, Shopify could ship it as a merchant feature, Meta could bundle it into Ray-Ban OS. The technical insight isn't a moat; it's a feature. Whoever has consumer distribution + brand catalog access wins, and that's not a startup. Could a startup execute it better than incumbents? Maybe, but the success probability is small, and my appetite for re-entering this problem space is smaller still.

**Kept for the record because:** the wardrobe-scan + reverse-inference idea is genuinely a clean way to bootstrap fit data without brand cooperation, and that pattern (use the user's existing artifacts as labeled training data) likely transfers to other domains. Worth remembering.

## References

- [Project Aria (Aria Digital Twin, Aria Gen 2 Pilot datasets + Research Kit)](https://www.projectaria.com/) — public foundation for body-pose + egocentric body-vision modeling; lowers our model-build risk.
- [Meta Ray-Ban Display launch (Sept 2025)](https://about.fb.com/news/2025/09/meta-ray-ban-display-ai-glasses-emg-wristband/) — proves the on-lens-display + EMG-wristband UX needed for a frictionless guided capture.
- [Snap Spectacles developer program](https://www.spectacles.com/) — alternate distribution if Meta locks down body-data primitives.
- [OpenAI Agentic Commerce Protocol developer docs](https://developers.openai.com/commerce) — the integration target for Layer 1 (per-call fit query).
- [Coresight — True Cost of Apparel Returns](https://coresight.com/research/the-true-cost-of-apparel-returns-alarming-return-rates-require-loss-minimization-solutions/) — the buyer pain quantified.
- [Latent Space — Applied Intuition (Physical AI)](https://www.latent.space/p/appliedintuition) — tone reference: the bottleneck in physical-world AI is harness engineering, not model intelligence; relevant framing for "the model science is ready, the productization is the bet."

## Related

- [[Veracart — Cryptographic product cards that AI shopping agents can actually trust]] — sibling proto on the agent-mediated commerce stack; product-authenticity layer where Tessera is the fit layer.
- [[Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses]] — sibling glasses-as-sensor proto in a different vertical.
- [[Conviction — AI-populated forecasting markets for enterprise operations]] — sibling agentic-decision proto from the same kit theme.
