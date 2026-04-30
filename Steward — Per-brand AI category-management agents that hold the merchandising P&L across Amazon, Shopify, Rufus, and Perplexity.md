---
id: proto-steward
aliases:
  - Steward
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
proto_generator:
  seed: 30654284
  writer: 2
  writers_total: 2
  repo_sha: 2a7d0ef
  generated_at: 2026-04-30T19:32:00+00:00
---

# Steward — Per-brand AI category-management agents that hold the merchandising P&L across Amazon, Shopify, Rufus, and Perplexity

## What is it?

**Elevator pitch**: Steward sells a $5–25M-revenue DTC brand a *bespoke* AI category manager — one agent per brand, trained on that brand's own Shopify orders, Amazon Seller Central data, and competitor pages — that runs the everyday merchandising loop a human category manager used to run: which SKUs to add, which to retire, which titles and bullets to rewrite this week, which search terms to bid on, which prices to nudge. The brand pays for outcomes (incremental gross profit) rather than seats; the human merchant becomes a reviewer of the agent's daily PRs.

**How it works**: On install, Steward reads the brand's last 18 months of Shopify orders, Amazon Brand Analytics, ad-spend history, returns reasons, and the top 20 competitors' product pages. From that corpus it derives a per-brand merchandising "schema" — what categories the brand is actually competing in, what attributes drive conversion in each, what its win/loss patterns look like by retailer. A per-brand agent then runs a continuous loop: scrapes the digital shelf daily, opens GitHub-style merchandising PRs ("retire SKU-1142, write new A+ for SKU-2207, raise SKU-0918 from $34 to $37, add 'wide-calf' as a new variant axis"), and only ships once the brand merchant approves. Each PR carries its expected $ impact and the historical evidence base.

## What's the problem?

Mid-market DTC brands ($5–25M revenue) sit in the worst spot in commerce. They sell across Amazon, Shopify, Walmart, and increasingly Rufus and Perplexity, each with its own algorithm and merchandising surface. They cannot afford a real category-management team — that's a six-figure-per-head Amazon-trained skillset — so the work falls on a single overworked merchant or the founder, who reacts only when something breaks. Existing tools (Pacvue, Perpetua, Profitero) automate ad-bid optimization and surface analytics dashboards, but the *decisions* — what to stock, retire, rewrite, reprice — still require a human category manager translating those dashboards into actions. The brand is paying $695/month for the dashboard and absorbing the labor cost of acting on it.

## Why now (2026)

- **Shopping is now agent-mediated, and the agents have different decision criteria than humans.** Amazon's Rufus has been used by 250M shoppers in the past year, customers who engage with Rufus are 60% more likely to purchase, and Amazon attributes $10B in annualized incremental sales to it ([Amazon CEO Andy Jassy on Q3 2025 earnings call, via Yahoo Finance/Fortune](https://finance.yahoo.com/news/amazon-says-ai-shopping-assistant-152500992.html)). Perplexity Shopping launched free to all US users in November 2025 with PayPal-powered checkout and merchant-of-record retention for retailers ([Perplexity launch post](https://www.perplexity.ai/hub/blog/shopping-that-puts-you-first)). What ranks in those surfaces is not the same as what ranks in classic Amazon search.
- **Bespoke per-tenant software just became economical.** A SaaS like Lovable now sells a Pro plan at $25/month shared across unlimited users to spin up custom apps ([Lovable pricing](https://lovable.dev/pricing)). The same drop in build cost that makes per-user web apps trivial makes per-brand merchandising agents — each carrying its own brand's data schema and decision history — tractable to operate at scale.
- **a16z just publicly validated the "agent that owns the data schema" pattern in adjacent spend.** Their April 15, 2026 post announcing the Hilbert Series A frames the bet exactly: "an AI system that can learn a company's data schema, structure and label it, and then keep maintaining that foundation as the business evolves" — applied to growth ([a16z, Investing in Hilbert](https://www.a16z.news/p/investing-in-hilbert)). Hilbert took growth-ops; the same pattern in merchandising decisions is open.
- **Incumbents are explicitly racing to add agents but staying inside their existing wedges.** Pacvue launched Pacvue Agent in April 2026, focused on running and measuring Amazon ad campaigns and querying Amazon Marketing Cloud — explicitly "currently available only for Amazon Ads" ([Adweek on Pacvue Agent launch](https://www.adweek.com/commerce/pacvue-enters-ai-agent-race-with-amazon-focused-tool/)). The agent automates the *ad-buying* loop; it does not own the assortment, content, or pricing loops, and is not cross-retailer.
- **Retail-media ranking is converging on unified paid+organic logic.** Pentaleap's unified-ranking platform now runs at The Home Depot, Macy's, and CVS, with Macy's choosing them in January 2026 ([Macy's selects Pentaleap](https://retailtechinnovationhub.com/home/2026/1/22/macys-taps-pentaleap-technology-to-create-more-open-and-flexible-retail-media-ecosystem)). Retailer-side, the line between "which products win the shelf" and "which ads run" is dissolving — meaning brand-side category management increasingly *is* a single optimization problem across content, assortment, and bid, which a per-brand agent can finally hold end-to-end.

## Who else is doing this

- **AI-augmented retail-media ad managers** — main player: **[Pacvue](https://pacvue.com/)** (Pacvue Agent, April 2026, Amazon-only at launch per the [Adweek launch coverage](https://www.adweek.com/commerce/pacvue-enters-ai-agent-race-with-amazon-focused-tool/)). Others: [Perpetua](https://perpetua.io/) (Amazon and Walmart marketplace ad optimization, $695/mo entry plan per [Perpetua pricing guide on Atom11](https://www.atom11.co/blog/perpetua-pricing-guide)), [Trellis](https://gotrellis.com/) (positions itself as a "Profit Optimization Platform" for Amazon and Walmart sellers, ad + dynamic pricing). Their wedge is the ad bid; merchandising decisions (assortment, content, retirement) sit outside.
- **Digital-shelf analytics** — main player: **[Profitero+](https://www.profitero.com/)** (1,400+ retailer sites monitored, 9,000+ brands, now part of Publicis/Mars United). They produce the analytics layer and a chat-based "Ask Profitero" assistant; the *acting* on those analytics still falls on the brand's merchandising team.
- **Retail-media platform / unified ranking (retailer-side)** — main player: **[Pentaleap](https://www.pentaleap.com/)**. Macy's, The Home Depot, and CVS are clients. They fix the retailer's shelf; they are not a brand-side merchandising agent and never will be.
- **Product-data feeds for AI shopping channels** — main player: **[Productsup](https://www.productsup.com/agentic-commerce/)**, distributing optimized product feeds into ChatGPT, Perplexity, and Gemini surfaces. Adjacent to this bet — they own the syndication pipe; they don't make the merchandising calls (what to stock, what to retire) that the feeds reflect.
- **Adjacent agentic-growth bet (different vertical)** — **[Hilbert](https://www.a16z.news/p/investing-in-hilbert)** (a16z-backed Series A, April 2026), AI growth agents for consumer companies — same architectural pattern (per-customer schema-learning agent) applied to growth funnels rather than merchandising.

**Where the opening is**: Today's stack is fragmented along the seams of legacy job titles. Pacvue/Perpetua own "the ad-buyer's tool." Profitero owns "the analyst's dashboard." Productsup owns "the feed engineer's syndication." Pentaleap owns "the retailer's shelf." Nobody owns "the category manager's daily P&L decisions" across all of these surfaces — because a category manager was the human integration point. The opening is to be the agent that sits in that role: one per-brand model that ingests the brand's own outcomes, operates across channels, and outputs *decisions, not dashboards*. None of the incumbents will eat this from below — Pacvue is doubling down inside ads, Profitero will keep selling analytics into 9,000 brands, and Hilbert is in growth, not merchandising.

## Why us

- **Five years of Amazon Fashion category-management muscle, plus chief-of-staff exposure to how Amazon scales merchandising decisions to millions of SKUs.** Vincent has lived inside the exact decision loop this agent automates — which SKUs to add, retire, reprice, rewrite — at Amazon scale. Most "AI for retail" founders bring data-science depth and learn the merchandising ontology by reading. Vincent's edge is the inverse: knowing the ontology cold, knowing which decisions are load-bearing for category P&L, knowing which dashboards merchants ignore and why. That shapes both what the agent should automate first and which buyer language opens the door.

## Customer & buyer

- **Customer:** Head of E-commerce or VP Brand at a $5–25M-revenue DTC brand selling across Amazon + Shopify + (increasingly) Walmart, with a single overworked in-house merchant.
- **Buyer:** Same person, or the founder/CEO if no Head of E-commerce role exists. Budget line: rolled out of "merchandising tooling" or net-new from "we can't hire another category manager."
- **Champion:** The lone in-house merchant — the person currently triaging Profitero alerts and writing A+ content at 11pm. Steward turns their job from janitor to reviewer.
- **ICP test:** Selling on ≥2 marketplaces, ≥500 SKUs, currently paying for either Pacvue/Perpetua/Helium10 or a category-management agency, *and* the founder can name a missed merchandising decision (a SKU that should have been retired six months ago, a content rewrite that never shipped) from the last quarter.
- **Anti-customer:** Single-SKU brands (no category to manage). Pure-Shopify-only brands (no Amazon = the cross-channel wedge collapses). Enterprise CPGs already running Profitero+ + WPP Media — they have the team and the budget to keep doing it the old way.

## Wedge / where we could enter

- **Candidate A — "Retire and rewrite" weekly digest.** Free or $99/mo install: agent reads a brand's Shopify + Amazon data and ships a Monday-morning PR queue of "kill these 8 SKUs / rewrite these 12 listings / reprice these 5." Lowest-friction entry; lets us prove the schema-learning works before asking for the merchandising P&L.
- **Candidate B — Outcomes-priced category manager replacement.** $2k–$8k/mo flat for full agent operation across the brand's catalog, with a quarterly true-up tied to incremental gross profit. The bet here is that brands will pay for *operations*, not tooling, once they trust the agent's PRs.
- **Candidate C — Agentic-channel readiness audit.** One-shot $5k engagement: "your product data is 38% Rufus-ready, here's the gap." Lead-gen for A or B; uses Productsup-style feed analysis as the front door.

What pushes us toward Candidate B is buyer behavior at the design-partner stage: if early users default to *acting* on the digest PRs rather than treating them as analytics, the leap to outcome-pricing is short. If they treat digests as alerts and ignore the act-on step, retreat to A and figure out trust-building first.

## What makes it defensible

- **(a) Primary — per-brand merchandising memory.** Once the agent has 6–12 months of accepted/rejected PRs from a brand's merchant, it has a labeled dataset of *that brand's* merchandising preferences (margin floors, brand-voice constraints, SKU-rationalization tolerance) that no horizontal incumbent can replicate. Switching cost compounds with every approved PR. This is the Tessera-pattern transfer: the user's existing artifacts (their decisions) become the labeled training set.
- **(b) Secondary — cross-channel decision graph.** Steward sees how the same SKU performs across Amazon, Shopify, Walmart, Rufus, Perplexity. That cross-surface pattern is what lets it propose the *right* action (e.g., "retire on Walmart, double-down on Rufus") — and it's structurally outside Pacvue's reach (single-channel) and Profitero's reach (analytics, not actions).
- **(c) Year-3 endgame — the merchandising P&L line item.** If the agent owns the daily decisions and the outcomes are measurable, the next move is to take % of incremental gross profit instead of SaaS — which prices out tool incumbents and turns Steward into the brand's de facto category-management arm.

## How it could make money

| Layer                                  | Price range                                  | Comparable                                                    |
| -------------------------------------- | -------------------------------------------- | ------------------------------------------------------------- |
| **Layer 1 — Weekly digest**            | $99–$499/mo                                  | [Perpetua Essentials at $695/mo](https://www.atom11.co/blog/perpetua-pricing-guide) |
| **Layer 2 — Full agent operation**     | $2k–$8k/mo                                   | [Perpetua Growth Plan: $695/mo + % of ad spend](https://www.atom11.co/blog/perpetua-pricing-guide) |
| **Layer 3 (later) — % of GP uplift**   | 5–15% of measured incremental gross profit   | [Profitero+ enterprise contracts](https://www.profitero.com/) (custom, services-attached) |

Honest caveat on the business-model risk: the outcome-pricing layer (Layer 3) is where the venture-scale upside lives, and getting from Layer 2 to Layer 3 requires a clean attribution story brands trust. If we can't measure incremental gross profit cleanly enough that brands don't argue every quarter, the business stalls at Layer 2 — a healthy SaaS, but not a category-defining one.

## What would pressure the thesis

1. **Assumption:** Mid-market DTC brands will hand merchandising decisions to an agent rather than just to better dashboards.
   - **What would pressure it:** Design partners use the digest PRs as analytics ("nice to know") but don't act on them, and continue running merchandising calls through their human merchant.
   - **Lever:** Tighten the loop — give the agent the ability to *execute* approved PRs directly into Seller Central / Shopify Admin so the human cost of "act on the digest" approaches zero. If brands still won't act, retreat to a Profitero-shaped analytics positioning.
2. **Assumption:** Cross-channel (Amazon + Shopify + Walmart + Rufus + Perplexity) is a real wedge incumbents will not close.
   - **What would pressure it:** Pacvue's 2026 expansion roadmap (per [Adweek launch coverage](https://www.adweek.com/commerce/pacvue-enters-ai-agent-race-with-amazon-focused-tool/) they plan to extend Pacvue Agent beyond Amazon through 2026) lands fast, and they cover the same channels with a credible decision-layer not just an ad layer.
   - **Lever:** Lean harder on the *decision* surface (assortment, content, retirement) — Pacvue's DNA is media; if we own the merchandising decisions they'll buy us before they build them. Optimize for acquisition, not standalone scale.
3. **Assumption:** Per-brand bespoke agents are economically tractable to operate (the Lovable-economics bet).
   - **What would pressure it:** Local model costs for the daily scrape + decision loop turn out to be $500+/brand/month, eating Layer 1 margin entirely.
   - **Lever:** Pool the cross-brand category-knowledge layer (every Steward shares a base merchandising model; per-brand layer is just preferences + history) so per-tenant compute drops by 5-10x.
4. **Assumption:** Retailers won't lock down the data Steward needs (Amazon SP-API, Shopify Admin API, scrape access to competitor pages).
   - **What would pressure it:** Amazon tightens SP-API or competitor-scrape becomes adversarial enough to break the daily refresh.
   - **Lever:** Invest early in being a "good citizen" SP-API consumer; for competitor data, lean on Productsup-style retailer-friendly feeds and on the brand's own ad-platform data (which they already control).

## 2-week experiment

**Load-bearing assumption to test:** When a per-brand agent ships specific, $-impact-tagged merchandising PRs every Monday morning to a real DTC merchant, the merchant will *act on* — not just read — at least 40% of them within the week.

**Artifact to build (week 1):** A working "Steward Digest" agent for **one** real volunteer brand. Vincent ships an end-to-end pipeline (Amazon SP-API + Shopify Admin API + competitor-page scrape via webclaw + a small per-brand decision agent built on Claude with caching) that generates a Monday digest of 20–30 specific merchandising PRs, each tagged with expected gross-profit impact and the historical evidence base. Output is delivered as a shareable web page (Lovable-built) plus a Slack channel where the merchant can `/ship` or `/skip` each PR. Vincent ships the artifact in ~4 days using coding agents; one full day reserved for the volunteer-brand integration plumbing.

**Conversations (week 2):** 8 brand-side merchants / Heads of E-commerce at $5–25M DTC brands. Recruited from Vincent's INSEAD network (consumer-brand operator alumni), the Amazon Fashion alumni network, and 1–2 cold via LinkedIn. Each conversation opens with the live volunteer-brand digest on screen — *not* slides — and then walks through what they'd accept, reject, and want different in their own version. We do *not* pitch SaaS pricing; we ask what they'd pay for this output.

**Specific questions / asks:**
1. Looking at this Monday digest, mark each PR red/yellow/green for "would you ship this in your business this week?"
2. Of the green ones, what's the time-cost today of generating that decision yourself?
3. If we ran this for your brand, what's the outcome that would make you keep paying — number of PRs shipped, gross-profit lift, hours saved?
4. What data sources would you give us access to on day one vs. need legal review?
5. What's the closest thing you've evaluated and why didn't you buy it?

**Pass criteria (all three):** (a) The volunteer brand's merchant ships ≥40% of the digest PRs within the first 2 weeks of operation. (b) ≥3 of the 8 conversation brands ask to be the next design partner unprompted. (c) ≥1 of those 3 names a price they'd pay (any price) and a procurement timeline.

**Kill criteria:** Volunteer brand ships <20% of digest PRs in 2 weeks AND fewer than 2 of the 8 conversations want to continue. Either we mis-priced the human friction of acting on PRs, or merchandising-as-a-decision-loop isn't the buyer's mental model.

**Vincent's effort:** ~50 hours total. ~30 hours on artifact build (Vincent + coding agents), ~20 hours on the 8 conversations + write-up. Output: the live volunteer-brand digest URL + a memo with quoted answers + a go / pivot / kill recommendation on which wedge candidate (A, B, or C) to push into.

## What we don't know yet

- Whether agentic shopping surfaces (Rufus, Perplexity, ChatGPT Shopping) will publish brand-side analytics that let Steward measure per-channel performance, or whether they'll stay opaque and force us to infer from session-level Shopify data.
- Whether Shopify itself will ship a first-party "AI category manager" feature at the App Store tier, collapsing the small-brand end of the market into a $0 baseline.
- How much of the merchandising decision quality comes from the brand's own historical data vs. from competitor-page scraping — i.e., whether Steward's edge survives if competitor pages get harder to scrape.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Veracart — Cryptographic product cards that AI shopping agents can actually trust]]
- [[Stentor — Agent-native commerce surface for medical-imaging and lab-diagnostics vendors selling into hospitals where AI agents now sit on the buyer side]]
- [[Touchstone — Per-variant evals so the bespoke-software era doesn't ship a million silently-wrong internal tools]]
