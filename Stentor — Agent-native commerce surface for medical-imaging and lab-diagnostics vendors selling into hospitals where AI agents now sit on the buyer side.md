---
proto_generator:
  seed: 846313158
  writer: 3
  writers_total: 3
  repo_sha: 7c0132d
  generated_at: 2026-04-30T09:03:41+00:00
id: proto-stentor
aliases:
  - Stentor
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
---

# Stentor — Agent-native commerce surface for medical-imaging and lab-diagnostics vendors selling into hospitals where AI agents now sit on the buyer side

## What is it?

**Elevator pitch.** Stentor is a hosted product-and-quote surface that medical-imaging and lab-diagnostics vendors (Siemens Healthineers, GE HealthCare, Philips, Roche Diagnostics, Bio-Rad, Thermo Fisher) install in front of their existing dealer/quote portals so that when a hospital's procurement agent (or a GHX/Vizient-side replenishment agent) hits the catalog page, the page responds with the structured product, compatibility, regulatory-clearance, install-base-fit, and quote-window data the agent actually needs to recommend a purchase — instead of a marketing site designed for a human rep visit.

**How it works.** The vendor points a CNAME (`agents.siemens-healthineers.com`) at us; we ingest their existing PIM, CRM-held install-base, regulatory clearances (510(k)/CE/PMDA), consumables-compatibility matrices, and current quote-windows into a per-vendor knowledge graph that fuses these usually-siloed sources. Every catalog page gets a parallel agent-facing surface: structured product feeds in the OpenAI/Stripe Agentic Commerce Protocol shape ([github.com/agentic-commerce-protocol](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol)), MCP endpoints exposing the configurator and quote-spawn flow, and a generative-UI render that adapts to the agent's stated buying criteria (modality, slice count, throughput, budget cycle, install-base compatibility). When the agent asks "is this MAGNETOM compatible with our 2019 install-base of head coils, what's the FDA clearance status, and what's the 30-day quote price?", the surface returns a structured, vendor-authoritative answer with a one-call quote spawn — not a "schedule a demo" form. Vendors keep their existing rep-driven motion for human buyers; Stentor is the parallel channel for the agent traffic that's now arriving and bouncing.

## What's the problem?

Med-device and lab-diagnostics vendors run dealer-portal + rep-led sales motions optimized for hospital VPs of Procurement scheduling 6-month evaluation cycles. Hospital procurement teams have started deploying AI agents that scan catalogs, build comparison matrices, and pre-qualify vendors before a rep is even contacted — and Forrester predicts B2B procurement teams will deploy agents capable of "scaling negotiation across hundreds of suppliers simultaneously" in 2026 ([Mirakl/Forrester](https://www.mirakl.com/blog/top-5-ai-trends-in-b2b-reshaping-commerce-in-2026)). Today those agents land on a marketing page with no machine-readable catalog, no compatibility API, no quote endpoint — and either bounce or hallucinate a comparison. The vendor never knows the agent visit happened, and loses the slot in the hospital's shortlist.

## Why now (2026)

- **The agentic-commerce stack standardized in the last seven months.** OpenAI and Stripe shipped the Agentic Commerce Protocol with a 2025-09-29 initial release and a 2026-04-17 stable spec covering carts, feeds, orders, authentication, and MCP — explicitly designed for AI agents to discover, configure, and check out from sellers ([ACP repo](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol)). Stripe's seller documentation now treats "share product catalog with agents" as a first-class integration alongside human checkout ([Stripe agentic commerce docs](https://docs.stripe.com/agentic-commerce)). The pipes exist; almost no B2B vertical has wired into them yet.
- **YC just put the wedge in two of its Summer 2026 RFS slots.** "Software for Agents" by Aaron Epstein argues "the next trillion users on the internet won't be people, they'll be AI agents" and explicitly calls for software rebuilt agent-first; "Dynamic Software Interfaces" by Ankit Gupta calls for software whose UI is generated per-agent rather than one-size-fits-all ([YC RFS Summer 2026](https://www.ycombinator.com/rfs)). Both describe Stentor's surface from different angles.
- **Hospital and procurement-team agent adoption is no longer a hypothetical.** A B2B-trends roundup citing Gartner reports 80% of B2B sales interactions are already happening digitally and projects AI agents intermediating $15T in B2B purchases by 2028 ([Mirakl](https://www.mirakl.com/blog/top-5-ai-trends-in-b2b-reshaping-commerce-in-2026)); hospital group purchasing runs at Vizient-scale, with Vizient's "contract portfolio representing $156 billion in annual purchasing volume" per its own boilerplate in the Feb 2026 Spend Management Outlook release ([Vizient via Morningstar/BusinessWire](https://www.morningstar.com/news/business-wire/20260203151847/vizient-pharmacy-inflation-slows-while-it-construction-and-facilities-accelerate)). The AI agent share of that flow inflects this year.
- **The incumbents are building the pipes but not the agent-readable surfaces.** GHX runs the dominant healthcare e-procurement exchange (transaction automation, vendor credentialing, marketplace) but its solutions are still cataloged for human procurement officers and their ERPs — value analysis, order automation, vendor credentialing, invoice and payment ([GHX](https://www.ghx.com/)). Siemens Healthineers' own Digital Marketplace exists but is a human-browseable catalog of digital-health apps, not a machine-readable feed of imaging hardware compatibility ([Siemens Healthineers Digital Marketplace](https://www.siemens-healthineers.com/digital-health-solutions/digital-marketplace)). The vendor-side agent surface is the gap.
- **Generative UI is shipping at the consumer frontier and will land in B2B catalogs next.** GPT-Image-2 + Codex now close the asset-loop inside coding sessions — "the GPT-Image-2 + Codex combo… you can iteratively use to generate assets WHILE you code" ([Latent Space, ImageGen on the Path to AGI](https://www.latent.space/p/ainews-imagegen-is-on-the-path-to)) — pointing toward surfaces that render *to the requester* rather than to a static template.
- **Med-device supply-chain pressure is making procurement agents the rational answer.** Vizient's Summer 2025 Spend Management Outlook projects medical supply chain costs to rise 2.41% in 2026, "driven by rising costs in IT services, capital equipment and surgical supplies" with projections "shaped partly by established tariffs as of April 2025" ([Becker's Hospital Review, citing Vizient](https://www.beckershospitalreview.com/supply-chain/medical-supply-chain-costs-to-increase-2-41-in-2026-vizient/)). Hospital CFOs are signing off on agent pilots because the headcount alternative is unaffordable.

## Who else is doing this

- **Healthcare e-procurement exchanges** — main player: **[GHX](https://www.ghx.com/)** (the dominant healthcare supply chain platform; runs Exchange Enterprise, marketplace, vendor credentialing, value analysis). Others: **[Vizient](https://www.morningstar.com/news/business-wire/20260203151847/vizient-pharmacy-inflation-slows-while-it-construction-and-facilities-accelerate)** (per its own boilerplate, $156B annual purchasing volume, GPO-anchored). They sit *between* hospital and vendor and own the procurement officer's screen — but their surface is built for human procurement workflows + ERP integration, not for a hospital-side AI agent that wants a structured catalog query against the manufacturer. They will eventually expose agent endpoints, but as buyer-side aggregators with a procurement-officer mental model — they cannot give a vendor brand-controlled, configurator-grade detail without restructuring their neutrality.
- **Generic agentic-commerce protocol layers** — main players: **[Agentic Commerce Protocol (OpenAI + Stripe)](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol)** and **[Stripe agentic commerce](https://docs.stripe.com/agentic-commerce)**. These are the rails Stentor *uses*, not competitors — they ship a protocol and reference implementation aimed at consumer-grade and SMB merchant catalogs (the OpenAI commerce docs cover product feeds, file-upload, promotions). They explicitly do not ship the vertical knowledge graph (DICOM specs, 510(k) clearance ledger, install-base compatibility) that med-device agent buyers need.
- **B2B AI-catalog platforms** — main player: **[Mirakl Catalog Manager](https://www.mirakl.com/products/mirakl-catalog-manager)** (ingests supplier formats and outputs agent-ready content; pitched at marketplace operators). Others: **[BigCommerce B2B](https://www.bigcommerce.com/articles/b2b-ecommerce/ai-in-b2b-ecommerce/)**. Horizontal — they treat all SKUs the same and have no opinion about regulatory clearance lifecycles, install-base compatibility matrices, or hospital capital-equipment quote windows.
- **Vendor-owned digital marketplaces** — main player: **[Siemens Healthineers Digital Marketplace](https://www.siemens-healthineers.com/digital-health-solutions/digital-marketplace)** (curated catalog of digital-health apps; one-time / pay-per-use / subscription). Roche, GE HealthCare, Philips run analogous portals. They are first-party stores for their own digital products — not a generalized agent-readable surface across hardware, consumables, service contracts, and regulatory metadata. The vendor doesn't want to rebuild this stack themselves; they want to install it.
- **Procurement-side AI agents (the buyers we'd serve)** — examples: **[Ramp's procurement agents](https://www.pymnts.com/news/b2b-payments/2026/ramp-launches-ai-agents-to-automate-corporate-procurement/)** for corporate spend; ChatGPT/Perplexity used by procurement teams for product discovery (per Mirakl above). These are the *demand side* — they are the agents pinging the vendor's catalog and finding nothing structured to consume.

**Where the opening is.** The pipes (ACP), the buyer-side agents (Ramp, ChatGPT-as-procurement-tool), and the procurement exchanges (GHX, Vizient) are all moving — but none of them owns the **vendor-controlled, regulatory-aware, install-base-aware product surface** that an agent needs to make a high-confidence recommendation in a regulated, capital-equipment buying cycle. Horizontal catalog tools don't speak DICOM or 510(k); exchanges sit on the wrong side of the transaction; vendors don't want to build this themselves. Stentor is the agent-side surface a vendor's CMO/Head of Digital installs to stop being invisible to inbound agent traffic in their own category.

## Why us

- **Vincent has the rare three-way overlap this bet needs: 4 years inside Siemens Healthineers (2y technical sales for medical imaging, 1y CRM, 1y marketing) — he speaks the buyer's language and has scar tissue from the actual quote-and-RFP motion — *plus* hands-on experience building a knowledge-graph trend-analytics product at Amazon that fused heterogeneous data sources, *plus* coding-agent fluency to ship the agent surface solo.** Most founders attacking agentic commerce will come from horizontal e-commerce (Mirakl/Shopify world) or pure infra (ACP-spec contributors); they will struggle to sell to a Siemens product manager who needs to hear the right vocabulary about CT slice configurations and dealer-channel conflict before opening the door. The combination is asymmetric for THIS vertical.
- **INSEAD multi-language cohort + EN/FR exposure makes Europe (where Siemens, Philips, Roche, B. Braun are HQ'd) a natural first sales geography rather than a stretch.**

## Customer & buyer

- **Customer:** Director of Digital / VP Digital Sales / Head of E-Commerce at a Tier-1 or Tier-2 medical-imaging or in-vitro-diagnostics manufacturer ($1B+ revenue): Siemens Healthineers, GE HealthCare, Philips, Roche Diagnostics, Bio-Rad, Beckman Coulter (Danaher), Thermo Fisher, Hologic.
- **Buyer:** Same role plus the **CMO / Chief Commercial Officer** for budget sign-off. Budget line: digital channels / commercial transformation. Typical ACV: **$200k–$500k year-1**, growing with SKU coverage and number of agent-channels integrated.
- **Champion:** The **digital product manager** who currently owns the dealer portal or e-commerce site and is being asked by their CCO "are we showing up in ChatGPT shopping?" or "what happens when the hospital's procurement agent queries our catalog?"
- **ICP test:** ≥$1B revenue + ≥1 product line where hospitals do non-trivial pre-purchase research + an existing PIM / CRM / install-base system that can be ingested + the digital team has been asked at least one "are we ready for agent buyers?" question by the C-suite in the last 90 days.
- **Anti-customer:** Pure-rep, no-digital-channel companies (won't believe agents are arriving); pure-consumables shops where the buying decision is already auto-replenishment via GHX/Cardinal (the exchange owns the workflow, no vendor surface needed); regulated buyers whose primary motivation is compliance/audit (motivation kill — they should buy a different product).

## Wedge / where we could enter

- **Candidate A — Imaging-modality configurator surface for one Siemens Healthineers product line (e.g., MAGNETOM MRI).** A single design-partner contract with Siemens Healthineers' digital team to expose one modality's configurator, install-base compatibility, and quote-spawn through ACP + MCP. Narrowest scope, highest learning velocity, founder has buyer fluency in this exact org. Likely first move.
- **Candidate B — Lab-diagnostics consumables-compatibility surface for Roche Diagnostics or Bio-Rad.** Higher repeat-purchase volume, simpler install-base model, but the buying decision is already mostly auto-replenishment and Stentor adds less value. Useful if A doesn't materialize.
- **Candidate C — Multi-vendor surface bundled by a regional dealer/integrator.** Sells to a dealer (e.g., a European med-device distributor) who needs all their lines to be agent-readable for their hospital customers' agents. Faster aggregate revenue but founder-fit is weaker (dealer dynamics, not manufacturer).

What would push us toward A: a warm intro into Siemens Healthineers' digital team and a real "we got asked about agent visibility at the last QBR" pull. What would push us toward B: a Roche/Bio-Rad inbound first.

## What makes it defensible

- **(a) Primary — per-vendor knowledge graph stitched from PIM + CRM-held install-base + regulatory ledger + consumables-compatibility matrices is genuinely hard to assemble and grows more valuable with every integration.** This is exactly the heterogeneous-data-fusion problem Vincent built at Amazon (multi-source knowledge graph for trend analytics) — and the reason a vendor can't get this from a horizontal catalog tool. Six months in, the graph encodes the vendor's own product semantics in a way that takes a competitor a multi-quarter rebuild to match.
- **(b) Secondary — agent-channel relationships compound on the demand side.** Once integrated with ChatGPT, Perplexity, Ramp procurement agents, and the next two surfaces that emerge, switching cost rises sharply for the vendor: re-integrating each downstream agent platform via a new vendor is a multi-month project the digital team won't do absent a fire.
- **(c) Year-3 endgame — the federated query layer between hospital procurement agents and the top ~30 med-device manufacturers.** Once we sit on enough vendor surfaces, hospital-side agents prefer to route through Stentor (one shape, all vendors). At that point the moat flips from per-vendor data to two-sided network — and vendors who haven't installed have no choice but to.

## How it could make money

| Layer                                                  | Price range                            | Comparable                                                                                                                                                         |
| ------------------------------------------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Layer 1 — Vendor SaaS subscription**                 | $200k–$500k/yr per org                 | [Mirakl Catalog Manager](https://www.mirakl.com/products/mirakl-catalog-manager) (enterprise B2B catalog tier, custom-quoted in the same range)                    |
| **Layer 2 — Per-quote-spawned consumption**            | $5–$50 per agent-spawned quote         | [Stripe agentic commerce](https://docs.stripe.com/agentic-commerce) machine-payment + per-transaction model, applied to high-ticket capital-equipment quote events |
| **Layer 3 (later) — GHX/Vizient-side dealer revshare** | undefined % of agent-routed deal value | [GHX](https://www.ghx.com/) and exchange-side transaction-fee model (template — actual share TBD with first dealer partner)                                        |

**Honest caveat.** Layer 3 depends on Stentor reaching enough agent-side traffic to be worth a revenue share to GHX or a regional dealer; this is a 2027+ play and could be commoditized if GHX builds equivalent agent-routing in-house. Layers 1+2 stand alone.

## What would pressure the thesis

1. **Assumption:** Hospital procurement teams will deploy AI agents at meaningful volume against med-device catalogs in 2026–2027 (not 2029–2030).
   - **What would pressure it:** Mid-2027, fewer than 5% of Tier-1 hospital systems have a procurement agent in production hitting external vendor catalogs; the agent-buyer share of inbound RFPs at a design-partner vendor is below 2%.
   - **Lever:** Pivot from "passive surface for inbound agents" to "outbound: package the same data graph as a vendor-owned procurement-team-facing agent that *vendors* deploy at hospital prospects." Same data foundation, different go-to-market.
2. **Assumption:** Med-device vendors will pay $200k+ for an agent-channel surface rather than build it in-house with their digital team.
   - **What would pressure it:** Siemens / GE / Philips digital teams ship in-house ACP feeds in 2026 (likely cheap-to-build at the schema level) — the vendor concludes Stentor is just product data and prompt engineering.
   - **Lever:** Defend the knowledge-graph layer (regulatory + install-base + consumables-compatibility fusion is the real work, not the ACP wrapper) and price for that. Possibly OEM the graph layer back to the vendor and price as a build-vs-buy escape hatch.
3. **Assumption:** GHX / Vizient will not be first to ship the agent-readable surface that subsumes this entire wedge.
   - **What would pressure it:** GHX announces an "agent-ready exchange" in 2026 — vendor product data already lives there and they have the procurement-officer relationship.
   - **Lever:** Position Stentor as the *vendor-controlled* surface, brand-authoritative and configurator-grade, vs. GHX's neutral-aggregator surface. Most vendors will want both, just as they fund both their own dealer site *and* their GHX feed today.
4. **Assumption:** The agent demand side (ChatGPT shopping, Perplexity, procurement-side agents like Ramp) will reach Stentor-served catalogs at meaningful query volume rather than route via a dominant aggregator.
   - **What would pressure it:** ChatGPT shopping becomes the only meaningful inbound channel and routes exclusively through GHX-style aggregators in regulated verticals.
   - **Lever:** Become the connector that publishes the vendor surface *into* whichever aggregator dominates — sell vendors on the surface, not the channel.

## 2-week experiment

**Load-bearing assumption to test:** Will the digital-product-manager / Head of Digital at a Tier-1 medical-imaging vendor look at a working agent-readable surface for one of their own SKUs and say "this is a problem we already know we have, what's the procurement path" — vs. "interesting, come back when agents are real"?

**Artifact to build (week 1).** A live, public **agent-queryable demo surface** for one publicly-documented Siemens Healthineers MAGNETOM MRI line, pulling from public spec sheets + 510(k) database + a synthetic install-base compatibility matrix:
- Hosted at `stentor-demo.com/magnetom`.
- Exposes (a) an Agentic Commerce Protocol-shaped product feed JSON, (b) an MCP server with `get_compatibility(install_base_id)` and `spawn_quote(config, hospital_profile)` tools, (c) a side-by-side render: human-facing marketing page on the left, generative-UI agent-facing render on the right that adapts to the agent's stated buying criteria (modality, slice count, throughput, budget cycle).
- Plus a 90-second screencast: an agent (Claude with MCP) queries the surface, retrieves the compatibility matrix, generates a comparison table, and spawns a structured quote — all in one turn. The screencast is the conversation prop; without it the meeting is a slide deck about a future thing.
- Built solo by Vincent in ~5 working days using Claude Code + ACP reference implementation + scraped public spec sheets. No real Siemens partnership needed for the demo.

**Conversations (week 2).** **8 conversations** with target buyers, each opening with the screencast, then a hands-on agent-query demo:
- 5 with digital-product / e-commerce / digital-sales leads at Tier-1 imaging or IVD vendors (Siemens Healthineers via Vincent's network, GE HealthCare, Philips, Roche Diagnostics, Bio-Rad).
- 2 with hospital-side procurement leads who have started AI-agent pilots (any large IDN; intro via INSEAD healthcare alumni).
- 1 with a GHX or Vizient product person to pressure-test the "exchange will subsume this" thesis directly.

**Specific questions / asks** (each answerable in 30 minutes with the artifact open):
1. "Looking at this surface — does it answer the question your boss is currently asking you about agent-buyer readiness? If not, what's missing?"
2. "If we built this for your top-3 product line, what would you need to see in pilot to expand to all lines?"
3. "Does your digital team have the bandwidth and PIM access to do this in-house, or would you rather outsource the data fusion?"
4. "What's your install-base data quality like today — could we even ingest it cleanly?"
5. (To hospital-side) "When your procurement agent queries a vendor catalog and gets nothing structured, what does it currently do?"
6. (To GHX/Vizient) "Are you planning an agent-readable feed in 2026? Would you partner with a vendor-side surface vendor or build in-house?"

**Pass criteria.** ≥3 vendor-side LOIs (intent to pilot) AND ≥1 vendor pulls out a Q3-2026 pilot budget AND the screencast gets ≥X organic shares from a posted LinkedIn / YC RFS-tagged tweet (≥50 reactions, ≥3 inbound from named ICP companies).

**Kill criteria.** ≤1 LOI; OR all 5 vendor-side conversations say "we'll build this in-house with our PIM team in Q3"; OR hospital-side conversations reveal procurement agents have not actually been deployed against external vendor catalogs at any of the queried IDNs.

**Vincent's effort.** ~50 hours, split ~30 build + ~20 conversations. Output: live artifact at `stentor-demo.com/magnetom` + screencast + memo with quoted answers + go / pivot / kill recommendation.

## What we don't know yet

- How much vendor PIM data is actually ingestable vs. trapped in legacy SAP / Oracle systems with no API. The discovery cost on integration #1 may dwarf the rest.
- Whether the install-base data (which lives in CRM and is highly sensitive) is something the vendor will let us touch in year 1 — or whether we have to start with the public catalog half and earn install-base access later.
- Whether ACP itself will fragment by vertical (a "healthcare ACP profile") or remain a single horizontal spec — affects how much vertical schema work we shoulder vs. inherit.
- Whether hospital-side procurement agents prefer to route through GHX-style aggregators (one auth, one schema) or directly to vendor surfaces (richer data, brand-authoritative). The honest answer probably depends on category — capital equipment direct, consumables aggregated.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Veracart — Cryptographic product cards that AI shopping agents can actually trust]]
- [[Veil — Privacy-preserving authorization mandates for AI checkout agents]]
- [[Bookmaker — Settlement-grounded routing markets that turn every CI run into a calibrated bet on which model should do the work]]
- [[Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses]]
