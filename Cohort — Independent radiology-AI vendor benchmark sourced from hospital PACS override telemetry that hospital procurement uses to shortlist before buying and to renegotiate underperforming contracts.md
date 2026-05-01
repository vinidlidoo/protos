---
id: proto-cohort
aliases:
  - Cohort
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
proto_generator:
  seed: 7734679
  writer: 2
  writers_total: 3
  repo_sha: aba8ddf
  generated_at: 2026-05-01T06:03:27+00:00
---

# Cohort — Independent radiology-AI vendor benchmark sourced from hospital PACS override telemetry that hospital procurement uses to shortlist before buying and to renegotiate underperforming contracts

## What is it?

**Elevator pitch.** Hospital radiology AI procurement is buying blind: vendors publish their own RCT numbers and there is no neutral source that says "Aidoc PE-detection vs. Annalise CXR vs. Gleamer fracture, on a scanner-mix and case-mix that looks like *yours*." Cohort sells radiology departments and integrated-delivery-network procurement teams a vendor-comparison subscription, sourced from override telemetry that already exists inside their own PACS/RIS audit logs and a multi-site peer cohort that lets us normalize for population and equipment. Customers use it to shortlist before signing seven-figure enterprise contracts, and to claw back pricing on contracts where their own override data shows the model isn't earning its keep.

**How it works.** A small on-prem connector reads PACS DICOM SR/GSPS objects, RIS report-state changes, and per-radiologist worklist actions (accept-flag, dismiss-flag, edit-after-accept, escalate). We extract per-finding concordance and override events at study granularity, normalize by scanner manufacturer, protocol, and case-mix using shared schemas across our customer cohort, and surface a vendor scorecard that ranks deployed and candidate models on real-world sensitivity, override-quality, and turnaround-time impact for *that customer's* mix. Hospital procurement gets a benchmark API and quarterly scorecard PDF; vendors can buy site-blinded peer reports back. We never need vendor cooperation to start measuring.

## What's the problem?

Radiology AI enterprise contracts now run from the hundreds of thousands to over $1M annually for large health systems ([TechVernia](https://techvernia.com/pages/reviews/medical/aidoc.html)), and FDA has cleared 1,104 radiology AI devices through end-2025 with GE HealthCare, Siemens, Philips, Aidoc, and DeepHealth all consolidating fast ([The Imaging Wire, FDA Updates AI List](https://theimagingwire.com/2026/03/11/numbers-from-the-fda-show-radiology-is-maintaining-its-lead/)). Yet there is no neutral, site-specific evidence the buyer can use. Vendors quote their own retrospective AUCs (Annalise's chest-X-ray clearance rests on retrospective testing of 3,252 cases at four hospitals — [xrayinterpreter K250831](https://xrayinterpreter.com/fda/K250831)); CMIOs and rad-chairs run one-off pilots that don't compare across vendors and don't catch drift after go-live. The override pattern that would tell them "this vendor's PE flag flips 54% of the time on follow-up imaging" is sitting unread in their own PACS audit logs ([arXiv 2601.13379](https://arxiv.org/pdf/2601.13379)).

## Why now (2026)

- **The market is now consequential and crowded.** FDA cleared 1,104 radiology AI devices through end-2025 — 76% of all AI-enabled medical-device authorizations — with GE HealthCare at 120 cleared products, Siemens Healthineers at 89, Philips at 50, Canon at 45, Aidoc at 31, and DeepHealth at 28 ([The Imaging Wire, FDA Updates AI List](https://theimagingwire.com/2026/03/11/numbers-from-the-fda-show-radiology-is-maintaining-its-lead/)). When a category has hundreds of cleared products and a handful of vendors converging via acquisition, buyers need a comparison layer.
- **Override telemetry now produces academically-credible "real-world" deltas.** A 2026 Pulmonary-Embolism follow-up study found that when a radiologist overrides AI to diagnose PE, 54.2% of follow-up scans show both agreeing on no-PE — a quantitative signal of false-positive behavior invisible to vendor self-reporting ([arXiv 2601.13379](https://arxiv.org/pdf/2601.13379)). The override stream is becoming a recognized class of evidence.
- **Hospitals already capture the substrate but don't use it.** Modern PACS routes AI output as DICOM SR / GSPS objects with first-class audit trails, and orchestration vendors recommend running new models in shadow mode to log results before changing the worklist ([Medicai, AI Orchestration in PACS](https://blog.medicai.io/en/ai-orchestration/)). The data is in the PACS today; nobody packages it as a procurement signal.
- **A registry-level player (ACR Assess-AI) has validated the concordance pattern but punted on the buyer-decision use case.** ACR's Assess-AI registry compares deployed-AI output to LLM-extracted "surrogate ground truth" from radiology reports for a national QA/QI benchmark, priced $1,500–$12,500/yr by site count and rad count ([ACR Assess-AI FAQ](https://nrdrsupport.acr.org/support/solutions/articles/11000129782-assess-ai-faqs)). The registry is positioned as accreditation/QI, not as procurement leverage — the comparison-shopping job is left open.
- **The first commercial entrants are framing themselves as compliance, not procurement.** Radinate offers cross-vendor monitoring for hospitals but anchors on "FDA-grade compliance" and Joint-Commission/CHAI alignment ([Radinate](https://www.radinate.com/)). That framing wins governance committees but not procurement; CFOs and rad-chairs don't sign for "trust layers."
- **Hospital procurement itself is going agentic — and agents need an API to call.** MedReddie has $2M in funding to automate hospital RFx generation and is partnered with HealthPRO Canada ([MedReddie](https://medreddie.com/)); AMS Health pitches AI agents that "discover product alternatives" with "compare options side-by-side with standardized data" ([AMS Health](https://www.amshealth.ai/)). When a procurement agent on a CIO's behalf shortlists imaging-AI vendors, it will call the benchmark with the best buyer-side data — that endpoint should exist, and it should be ours.
- **Liability pressure is making the override stream load-bearing for the rad chair, not just QI.** A 2026 Nature Health mock-jury study found participants were 2.6× more likely to side with the plaintiff in a single-read AI workflow vs. double-read (74.7% vs. 52.9% pro-plaintiff) ([Bernstein et al., Nature Health 2026](http://www.nature.com/articles/s44360-026-00085-2)). A rad chair who can't quantify override-quality across vendors can't defend the workflow choice in malpractice; we make that defensible.

## Who else is doing this

- **Quality-registry incumbent — the ACR's [Assess-AI registry](https://nrdrsupport.acr.org/support/solutions/articles/11000129782-assess-ai-faqs)**. Compares deployed AI output to LLM-extracted findings from the radiology report text and benchmarks against national peers. Positioned as QA/QI for the rad chair's accreditation file ($1,500–$12,500/yr by site/rad count). Doesn't deliver site-specific vendor *bake-offs*, doesn't model case-mix-normalized performance for *prospective* purchases, and the LLM-extracted "surrogate ground truth" misses mid-workflow override telemetry (dismissed flag, edit-after-accept, escalation). The ACR is also a professional society, not a hospital-procurement vendor — its incentive is registry scale, not buyer leverage.

- **Compliance-framed monitoring — main player: [Radinate](https://www.radinate.com/)**. Cross-vendor monitoring with FDA PCCP and Joint-Commission alignment. Sells to AI-governance committees on "trust but verify." That framing earns CMIO sign-off but not the procurement budget; the buyer is the CMIO/quality-officer, not the rad chair or supply-chain VP. They are not reframing the data into a vendor-comparison product.

- **Vendor-side AI orchestration — [Medicai](https://blog.medicai.io/en/ai-orchestration/), [RamSoft](https://www.ramsoft.com/blog/integrate-ai-with-ris-pacs)**. PACS-adjacent orchestration vendors that route studies, run shadow deployments, and log audit trails. They control the data pipe but their incentive is to sell the orchestration layer to the hospital and embed marketplace partners — not to publish neutral comparative scorecards that could embarrass those partners.

- **EHR-native AI monitoring — [Bayesian Health](https://www.bayesianhealth.com/platform)**. Built-in governance layer that "tracks performance in the real world and detects drift and bias" — but Bayesian is itself the AI vendor, not a Switzerland; their governance dashboard cannot serve as cross-vendor procurement leverage by definition. Useful precedent for the substrate, not a competitor for the wedge.

- **Healthcare-procurement agents — [MedReddie](https://medreddie.com/), [AMS Health](https://www.amshealth.ai/), [Procurai](http://procurai.polsia.app/)**. Replace the manual RFx process for hospitals; live with HealthPRO Canada and supplier partnerships. They generate purchase decisions but have no first-party imaging-AI performance data — they're customers of a benchmark, not competitors to one.

- **Generic clinical-AI labelers — [Centaur Labs](https://www.centaurlabs.com/post/our-data-driven-approach-to-qa)**. Sell expert-annotated ground truth to AI vendors for training/eval. Vendor-side, not buyer-side; not in the procurement loop.

**Where the opening is.** The data substrate (PACS override telemetry + cross-site cohort) and the buyer (hospital procurement, rad chair, supply-chain VP) are mutually orphaned: ACR owns the substrate but sells QI; Radinate owns a buyer but sells compliance; orchestration vendors own the pipe but won't bite the partners that pay them. A neutral procurement-anchored product — sold on "you're about to spend $1M on three competing models, here's the bake-off scorecard for *your* scanner mix and case mix, and here's the renegotiation memo for your underperforming current vendor" — is where no incumbent is structurally aligned to land.

## Why us

- **Vincent walked both sides of the imaging-vendor sales door at Siemens Healthineers (2y technical sales, 1y CRM, 1y marketing).** He knows what the vendor's clinical-evidence stack actually is, what numbers a hospital procurement office trusts vs. dismisses, and how an enterprise imaging contract gets clawed back. That's the asymmetry: most healthtech founders attack this from the AI side and get bounced by the hospital procurement workflow; Vincent can architect the data-back-to-buyer contractual terms that hospitals will actually sign because he has lived inside the vendor's commercial machine.

## Customer & buyer

- **Customer:** Chief of Radiology / Imaging Service Line VP at integrated delivery networks (IDNs) and academic medical centers with active radiology-AI deployments across ≥3 vendors.
- **Buyer:** Supply-Chain VP / VP Strategic Sourcing for clinical IT, often co-signing with the rad chair. Budget line: imaging-AI procurement and renewal. Typical ACV $80K–$250K for a multi-site IDN.
- **Champion:** the rad chair's data-science liaison or the imaging informatics director — the person who has tried to manually pull override stats once and given up.
- **ICP test:** ≥3 deployed FDA-cleared radiology AI products from different vendors, ≥1 contract renewal in the next 12 months, willing to license de-identified PACS audit logs back to a third party with a BAA.
- **Anti-customer:** Single-vendor shops, hospitals on closed enterprise-imaging deals where the AI is bundled by the PACS vendor (no procurement leverage exists; they're locked in by contract). Also: any hospital where the rad chair's incentive is to defend the existing vendor choice rather than renegotiate it.

## Wedge / where we could enter

- **Candidate A — "PE-detection bake-off" for stroke/PE workflows.** Single, high-volume, financially-consequential finding category (Aidoc, Viz.ai, RapidAI all compete here). Easy to demonstrate: pull six months of CTPA studies and PE-flag override events from a single design partner, deliver the comparative scorecard. Pushes us here if early customers prioritize stroke-team workflow optimization, where the override consequences are most quantified academically.
- **Candidate B — "AI contract renewal defense memo."** Land at the moment of an upcoming renewal: 90-day engagement, deliver a renegotiation memo grounded in their own override data. Highly time-bound, immediately ROI-legible. Pushes us here if early conversations show that buyers don't act on continuous monitoring but do act on contract events.
- **Candidate C — "Imaging-AI shortlist API for procurement agents."** Sell directly into the agentic-procurement layer (MedReddie-class) as the imaging-AI benchmark backend their agents call. Pushes us here if procurement-agent vendors mature faster than expected and are willing to pay per call rather than the hospital paying per scorecard.

Default opening is Candidate B — a 90-day "renewal-defense" engagement with a single design-partner IDN, then convert into a recurring scorecard subscription. Renewal-defense is the cheapest call to action; once the data pipeline is in, the recurring benchmark and the procurement-API layer are nearly free to add.

## What makes it defensible

- **(a) Primary — multi-site case-mix-normalized cohort data.** Each new IDN customer adds a scanner-fleet × population × protocol slice to a shared normalization model that lets us tell *any* customer "your override rate vs. peer cohort with similar scanner mix." That comparison cannot be reconstructed by either ACR (which doesn't capture mid-workflow override telemetry) or any single vendor (who only sees their own deployments). The data flywheel compounds linearly with site count.
- **(b) Secondary — neutrality moat.** ACR, PACS-marketplace orchestrators, and AI-vendor-owned monitoring tools all have structural conflicts that make them unwilling to publish vendor-by-vendor scorecards. Cohort's commercial position depends on doing exactly that. Hospitals will trust the ranking *because* we have no vendor partnership revenue to defend — and we will visibly turn down any vendor offer that creates one.
- **(c) Year-3 endgame — the procurement-agent benchmark API.** As MedReddie/AMS-class agents mature into the default RFx workflow, the imaging-AI benchmark API they call becomes the system of record for "should we buy this." Owning that API turns Cohort from a scorecard-PDF subscription into procurement-flow infrastructure.

## How it could make money

| Layer                                                               | Price range                     | Comparable                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Layer 1 — Renewal-defense engagement (90 days)**                  | $40K–$80K one-time              | [KLAS](https://klasresearch.com/membership-options) Decision Insights / advisory tier                                                                                                                                                                                                                                     |
| **Layer 2 — Quarterly comparative scorecard subscription**          | $80K–$250K/yr per IDN           | [ACR Assess-AI](https://nrdrsupport.acr.org/support/solutions/articles/11000129782-assess-ai-faqs) ($1.5K–$12.5K/yr at site/rad scale) sets the floor; commercial buyer-leverage product brackets above                                                                                                                   |
| **Layer 3 (later) — Per-call benchmark API for procurement agents** | $0.50–$5 per shortlist API call | [Aidoc](https://aws.amazon.com/marketplace/pp/prodview-hmy5pemibugck) lists $6 per scan per algorithm per site on AWS Marketplace; AI-vendor enterprise contracts run [hundreds of thousands to over $1M annually](https://techvernia.com/pages/reviews/medical/aidoc.html) — bracketing the unit economics on either end |

Honest caveat: the renewal-defense layer risks looking like a consulting engagement if we don't productize the connector and scorecard fast. Layer 2 only earns the price if Layer 1 customers stay engaged after their renewal date passes — we should target IDNs with multiple staggered renewals across their network so subscription value compounds.

## What would pressure the thesis

1. **Assumption:** Hospital procurement has the willingness and authority to license PACS audit logs to a third party under a BAA, even when the PACS vendor or current AI vendor objects.
   - **What would pressure it:** Design-partner conversations stall on the BAA / data-egress clause; PACS vendors invoke contract terms preventing third-party telemetry export.
   - **Lever:** Pivot to an on-prem ACR-Connect-style appliance model where Cohort never receives PHI — only the normalized per-finding events flow back. Gives up some flexibility but matches the regulatory pattern hospitals already accept.

2. **Assumption:** ACR Assess-AI does not extend into procurement-decision use cases on a 24-month horizon.
   - **What would pressure it:** ACR launches a comparative shortlisting product or partners with HealthPRO/Vizient on procurement; the registry's surrogate-ground-truth method matures enough to replace mid-workflow override telemetry as a benchmark signal.
   - **Lever:** Lean harder on (i) override telemetry that registry text-extraction can't see (dismissed flag, escalation, edit-after-accept) and (ii) the procurement-agent API endpoint, where ACR's nonprofit-society structure won't follow.

3. **Assumption:** Override events from PACS audit logs carry enough signal-to-noise to differentiate vendors at site granularity, after normalizing for scanner mix and case mix.
   - **What would pressure it:** Pilot scorecards show vendor differences inside noise floor at IDN scale (<3 hospitals); cohort needs to be much larger before differentiation appears.
   - **Lever:** Combine override events with downstream outcome reconciliation (follow-up imaging concordance, like the PE study's 54.2% transition signal) and turnaround-time deltas. Lower-bound differentiation may come from the latter even when override-rate noise dominates.

4. **Assumption:** PACS vendors and AI vendors don't coordinate to lock the audit-log substrate behind contractual exclusivity.
   - **What would pressure it:** Major PACS vendor (Sectra, GE Centricity, Change/Optum, Philips Vue) ships a "vendor-neutral monitoring marketplace" that contractually requires customers to route AI telemetry through it.
   - **Lever:** Race to get neutrality-clause language into customer contracts as standard procurement boilerplate before the lock-in happens. Vincent's vendor-sales fluency is the unlock here — knowing how those clauses get drafted and what hospital legal will hold the line on.

## 2-week experiment

**Load-bearing assumption to test:** That an IDN with ≥3 deployed radiology-AI vendors will (a) export 90 days of PACS audit-log + DICOM SR/GSPS data under a BAA to a third party, and (b) recognize the resulting bake-off scorecard as worth $40K–$80K of renewal-defense budget.

**Artifact to build (week 1).** A working "Cohort Scorecard" demo built from a public synthetic PACS audit-log corpus + the published per-vendor RCT numbers + simulated override telemetry, rendered as a real PDF + a live web dashboard. The demo must produce, for a hypothetical IDN with three named vendors deployed (Aidoc, Annalise, Gleamer), a one-page comparative scorecard normalized for scanner mix that shows: per-finding sensitivity, override rate vs. RCT-claimed performance, turnaround-time delta, and a renegotiation-leverage line ("here's what your contract should be paying"). Built solo by Vincent in ~5 working days using Claude Code: synthetic data generator + DICOM SR parser + scorecard renderer + simple Next.js dashboard hosted publicly. Linkable on a domain.

**Conversations (week 2).** 8–10 conversations: 3 with rad-chair / imaging informatics directors at IDNs (find via Vincent's Siemens Healthineers network), 2 with hospital supply-chain VPs (cold-source via [SBS NHS framework](https://www.sbs.nhs.uk/fas-artificial-intelligence-radiotherapy) listings or HealthPRO partner sites), 2 with procurement-agent founders (MedReddie, AMS Health), 2 with ACR-aware academic informaticists (potential advisors). Every conversation opens with the live scorecard URL on screen.

**Specific questions / asks.** With the scorecard visible:
1. Walk me through what your team would do with this scorecard for your next vendor renewal — what sections would you pull out?
2. Would you license 90 days of your PACS audit logs to a third party under BAA to populate this for your own IDN? If not, what would the appliance need to do for you to say yes?
3. What price feels right for a one-time renewal-defense engagement that ends with a memo like this? What price for a quarterly version?
4. If you saw a scorecard saying your current vendor is 12 points below the cohort median for *your* scanner mix, what's the next step at your hospital — and who needs to sign?
5. (To procurement agents) Would you call this as an API endpoint when shortlisting imaging-AI vendors for an RFx, and at what per-call price?

**Pass criteria.** ≥3 IDN signed letters of intent for a 90-day renewal-defense engagement at $40K+ AND ≥1 hospital agrees to share PACS audit-log data under a BAA for the first scorecard build AND ≥1 procurement-agent vendor commits to integrate Cohort as their imaging-AI benchmark backend AND public scorecard demo gets ≥10 inbound emails from hospital data-science / informatics roles.

**Kill criteria.** ≤1 LOI; or unanimous BAA-pushback ("legal will never let you receive that data"); or all five rad-chair conversations land on "we'd just call Aidoc and ask them to drop their price" rather than treating an external scorecard as the leverage tool.

**Vincent's effort.** ~50 hours: 25 hours building the artifact (synthetic data + parser + dashboard), 20 hours conversations, 5 hours synthesis memo. Output: the scorecard demo URL (publicly live), a memo with quoted answers from each conversation, a go / pivot / kill recommendation. Pivot path is most likely: "renewal-defense engagement is a yes, but go through procurement-agent vendor channel rather than direct hospital sales."

## What we don't know yet

- Whether PACS vendors' standard hospital contracts already preclude exporting per-radiologist override telemetry to third parties (and how negotiable that is at renewal time).
- Whether the override signal in PACS audit logs is rich enough to differentiate between two AI vendors at single-hospital scale, or only at multi-site cohort scale.
- Whether procurement-agent platforms (MedReddie-class) will pay for benchmark API calls or expect data partnerships in exchange for distribution.
- Whether ACR Assess-AI's registry distribution gives it enough data-flywheel head-start that we need to start in EU/Canada (where ACR's footprint is weaker) rather than US.
- Whether radiology AI vendors themselves become buyers (paying for site-blinded peer reports back) faster than hospitals do — a possible Layer-1.5 we haven't priced.

## Vincent's Feedback

1. **Pass on mission-pull, not idea-merit.** Healthcare is thorny enough that mission energy has to compensate for the regulatory drag and 12-24 month sales cycles. "Procurement-tooling for hospitals" is worthy but doesn't generate enough velocity for me to attract aligned talent and survive the slow feedback loops. Future protos in regulated domains should be screened on mission-pull, not just market opportunity.
2. **The Siemens-Healthineers asymmetry is genuinely rare and worth pursuing in *this* space — but isn't sufficient on its own.** Founder-market fit doesn't override mission-fit when the domain is slow.
3. **Writer should have led "what makes it defensible" with the cross-PACS cohort argument, not buried it.** When a platform owner (PACS vendor) controls the substrate but extracts rent from neutrality, the third-party benchmark's defense is aggregating *across* platforms. That's the structural answer to the "why won't a PACS vendor do this" question and it's the strongest moat claim in the deck.
4. **Vendor-attribution chain through PACS audit logs is the load-bearing technical risk and was omitted from "what we don't know yet."** UI aggregation, scanner-bundled AI, and per-PACS log-fidelity variation can break the substrate claim. Future protos in instrumentation/observability spaces should pressure-test whether the data chain preserves the attribution needed for the product to work — and surface it as a top-3 risk if it does.

## Related

- [[Stentor — Agent-native commerce surface for medical-imaging and lab-diagnostics vendors selling into hospitals where AI agents now sit on the buyer side]] — sells the *vendor* side of the same shift; Cohort is the buyer-side complement.
- [[Tessera — Fit-confidence API for agent-mediated apparel commerce trained on smart-glasses body capture]] — same "use the user's existing artifacts as the labeled training set" pattern (PACS overrides ↔ wardrobe scans).
- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]] — sibling "real-world performance vs. vendor-claimed numbers" wedge in a different domain.
