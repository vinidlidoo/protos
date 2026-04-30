---
id: proto-atelier
aliases:
  - Atelier
tags:
  - proto
type: proto
status: drafted
created: 2026-04-29
origin: ""
proto_generator:
  seed: 699040402
  writer: 1
  writers_total: 2
  repo_sha: 06b2dc0
  generated_at: 2026-04-30T04:23:31+00:00
---

# Atelier — Per-patient cognitive rehab apps generated for smart glasses from the patient's own home

## What is it?

**Elevator pitch**: Atelier sells outpatient neurorehab clinics a smart-glasses program for stroke and traumatic-brain-injury survivors where each patient's at-home rehab app is *generated for them* — built around their actual kitchen, their actual face-recognition deficits, their actual route to the corner store. The clinic prescribes a 12-week program, the patient wears Ray-Ban-class glasses an hour a day at home, and the therapist gets back objective recovery telemetry that maps cleanly onto reimbursable cognitive-rehab CPT codes.

**How it works**: After an in-clinic intake, the patient wears the glasses through their home for one structured 30-minute capture session. Atelier's pipeline turns that capture into a per-patient training app — bespoke object-finding tasks anchored on the patient's own cabinets, divided-attention drills set in their living room, prospective-memory cues tied to their actual morning routine. The capture, generation, and inference all run on the patient's glasses + a paired local-model edge box (no patient video leaves the home). The therapist's web dashboard shows time-on-task, accuracy curves, and a session-by-session narrative auto-generated from the on-device telemetry, formatted to drop into 97129/97130 progress notes.

## What's the problem?

Cognitive rehab today is generic. A speech-language pathologist or occupational therapist runs a stroke patient through paper-and-tablet exercises in a 45-minute clinic visit, sends them home with photocopied worksheets, and re-tests in two weeks. Adherence at home is low because the exercises feel disconnected from the patient's actual life — "name 10 animals" doesn't help you remember where you put your keys. Clinicians know transfer-of-training is the bottleneck (the gain in clinic doesn't show up at home), but they have no tool that delivers therapy *in the home environment* without buying a $30k VR cart that ships back when the patient is discharged. Penumbra, the leading immersive-rehab vendor, ended service for its REAL Immersive System in September 2024, leaving an opening at the at-home tier ([Penumbra REAL service end notice](https://www.penumbrainc.com/immersive-healthcare/)).

## Why now (2026)

- **Smart glasses are crossing the affordability threshold for prescribed home use.** Ray-Ban Meta starts at $224.25 today, and Meta has already shown a true-AR product prototype (Orion) it intends to ship to consumers ([Ray-Ban Meta pricing](https://www.meta.com/smart-glasses/), [Meta Orion announcement](https://about.fb.com/news/2024/09/introducing-orion-our-first-true-augmented-reality-glasses/)). A reimbursable rehab program no longer requires a $30k headset cart.
- **Bespoke per-user software is finally economical.** The default unit of software is shifting from "one shared product" to "a variant per user," because building, forking, and personalizing apps is cheap — Lovable's Pro plan is $25/month shared across unlimited users to spin up custom apps ([Lovable pricing](https://lovable.dev/pricing)). The same economics that make per-user web apps trivial make per-patient therapeutic content tractable.
- **Local models on consumer hardware now handle on-device generation and inference at quality.** April 2026's local-model roundup names Qwen 3.5, Gemma 4, GLM-5, MiniMax M2.7, DeepSeek V3.2, and GPT-oss 20B as broadly recommended for local deployment, with Qwen3-Coder-Next as the consensus local coding model ([Latent Space, AINews local models April 2026](https://www.latent.space/p/ainews-top-local-models-list-april)). On-device inference is what makes "patient's home video never leaves the home" feasible without compromising the therapy.
- **The category leader retreated.** Penumbra ended REAL Immersive service on September 30, 2024, removing the highest-profile immersive-rehab incumbent right as the form factor was becoming consumer-priced ([Penumbra REAL service end notice](https://www.penumbrainc.com/immersive-healthcare/)).
- **Stroke is a 795,000-events-per-year, $56.2B-cost market in the US alone, and it is the leading cause of long-term disability** ([CDC Stroke Facts](https://www.cdc.gov/stroke/data-research/facts-stats/index.html)). The cohort that needs cognitive rehab is large, identifiable, and reached through a small number of outpatient rehab networks.

## Who else is doing this

- **Immersive-rehab incumbents (VR / headset)** — main player: **[MindMaze](https://mindmazetherapeutics.com/)**, with MindMotion GO and MindPod, deployed in clinical settings and home. They are headset-and-controller based, generic-content, and the company has been pivoting toward drug-development as a "neurotherapeutics" play. Penumbra's [REAL Immersive System](https://www.penumbrainc.com/immersive-healthcare/) was the other leader and ended service in September 2024.
- **FDA-authorized digital therapeutics (game-based)** — main player: **[Akili Interactive](https://www.akiliinteractive.com/)**, makers of EndeavorRx (FDA-authorized for pediatric ADHD) and EndeavorOTC for adult attention. Tablet/phone game format, single shipped product per indication, no per-patient personalization beyond difficulty adjustment.
- **Ambient-AI clinician-documentation incumbents** — main player: **[Augmedix](https://www.augmedix.com/)** (now part of Commure), which captures exam-room conversation and generates clinical notes for the doctor — clinician-side, not patient-side, and not in the therapeutic loop. They own the "ambient AI in the clinical workflow" wedge for documentation but do not deliver therapy.
- **Home-rehab software (no glasses)** — generic worksheet apps and tablet-based cognitive training products across the category; none ship a per-patient generated program tied to the patient's environment.

**Where the opening is**: nobody combines (a) smart glasses as the delivery surface, (b) per-patient generated therapeutic content anchored to the patient's actual home, and (c) on-device generation that keeps home video private. Akili owns single-indication FDA-authorized games. MindMaze owns clinic-grade headset rehab and is moving toward drugs. Penumbra exited the immersive tier. Augmedix sits in the clinician documentation flow, not the patient therapy flow. The wedge is the at-home therapeutic tier with the patient-environment data the incumbents structurally do not collect.

## Why us

- **Neuroscience depth + Siemens hospital/lab buyer fluency are the rare combination this bet needs.** Cognitive rehab buyers (rehab medical directors, OT/SLP department heads) are the same buyer archetype Vincent sold imaging to at Siemens — clinical evidence first, procurement second, integration third. Most consumer-glasses-for-health founders bring one half. Adding genuine neuroscience domain knowledge to the technical-sales pattern is what turns "interesting demo" into a 12-week reimbursable program.

## Customer & buyer

- **Customer (user):** stroke / TBI / mild-cognitive-impairment patient prescribed outpatient cognitive rehab.
- **Buyer:** rehab medical director or OT/SLP department head at an outpatient neurorehab clinic or hospital-affiliated rehab unit.
- **Champion:** the lead occupational therapist or speech-language pathologist running cognitive caseloads who is frustrated that home-program adherence is killing their outcomes data.
- **Budget line:** clinic capex for the glasses-and-edge-box loaner pool + per-patient therapeutic content fee billed against the clinic's existing 97129/97130 reimbursement.
- **Typical ACV:** $30k–$60k per clinic in year 1 (loaner pool + ~50 patients) scaling with patient throughput.
- **ICP test:** outpatient rehab clinics that already bill cognitive-rehab CPT codes, run ≥40 stroke/TBI cognitive cases per quarter, and have a quality-metric or value-based-care contract that punishes poor functional outcomes.
- **Anti-customer:** in-patient acute rehab (wrong reimbursement, wrong therapy intensity, wrong device pattern), and pure-wellness "brain training" consumer apps (no clinical buyer, no reimbursement).

## Wedge / where we could enter

The narrowest first move is **post-stroke unilateral spatial neglect** — a well-defined deficit, a well-defined patient pool, well-validated outcome measures (Behavioral Inattention Test, Catherine Bergego Scale), and an obvious mismatch with paper exercises (the deficit is *spatial*, the worksheets are *flat*). A glasses-delivered program that re-trains attention in the patient's actual visual environment is the clean fit.

- **Candidate A — Post-stroke spatial neglect**: deficit is intrinsically spatial, glasses are the right modality, outcome measures are standardized. Strongest candidate.
- **Candidate B — Mild TBI / post-concussion attention rehab**: larger pool, sports-medicine entry path, but reimbursement is messier and outcomes are softer.
- **Candidate C — Early-stage MCI prospective-memory training**: largest market but slowest sales cycle (memory clinics, geriatricians) and weakest "deficit-modality fit" story for a first wedge.

What pushes us toward A: a defensible 12-week outcome story is what unlocks the rehab-director sale, and neglect gives us the cleanest one.

## What makes it defensible

- **(a) Primary — the per-patient environment dataset.** Every patient's capture session generates a labeled spatial-cognitive-task dataset that no incumbent has, because no incumbent puts a generation-grade capture pipeline in the patient's home. Aggregated across patients, this is the substrate for content quality compounding faster than any clinic-only competitor can match. This is the "use the user's own existing artifacts as the labeled training set" pattern — the patient's own kept furniture, cabinets, and routines are the revealed-preference signal — applied to therapy instead of commerce.
- **(b) Secondary — clinical-evidence flywheel.** A reimbursable program with structured outcome telemetry produces RCT-grade data as a byproduct. The first peer-reviewed publication showing functional-outcome lift vs. standard-of-care home programs is a procurement moat against any consumer-glasses entrant.
- **(c) Year-3 endgame — FDA De Novo / 510(k) authorization for the spatial-neglect indication, then content-platform expansion across cognitive-rehab indications.** The platform's per-patient generation pipeline is reusable across deficits; each new indication is a content + clinical-validation cost, not a new product.

## How it could make money

| Layer                                  | Price range          | Comparable                                                                  |
| -------------------------------------- | -------------------- | --------------------------------------------------------------------------- |
| **Loaner pool + setup (per clinic)**   | $20k–$40k year 1     | [MindMaze MindMotion GO](https://mindmazetherapeutics.com/) (clinical/home neurorehab system) |
| **Per-patient program (12 weeks)**     | $400–$900 / patient  | [Akili EndeavorRx](https://www.akiliinteractive.com/) (FDA-authorized prescription digital therapeutic for ADHD) |
| **Bespoke-content authoring tooling (later, for content partners)** | $25–$50 / mo (workspace, unlimited users) | [Lovable Pro / Business](https://lovable.dev/pricing) (bespoke-app generation tooling) |

The honest business-model risk is that reimbursement coverage for digital cognitive-rehab content is uneven across payers, and that early sales cycles look like a clinical-trial sale (long, evidence-heavy, low repeatability) before they look like a SaaS sale. Akili's history shows this is real — even with FDA authorization, payer coverage took years and remains incomplete. Plan: anchor the first 18 months on cash-pay rehab clinics in markets where outcome-based or value-based-care contracts already create budget for adjunctive therapy, and treat broad payer reimbursement as a year-2+ unlock rather than a year-1 prerequisite.

## What would pressure the thesis

1. **Assumption: Ray-Ban-class glasses (or near-term equivalents) have the camera, compute, and battery to capture a clinically usable home environment scan and run an hour-a-day therapeutic session.**
   - **What would pressure it:** capture sessions take >60 min or fail >30% of the time on real patient homes; glasses overheat or run out of battery within a 30-min therapy session; the on-device model can't handle dim residential lighting reliably.
   - **Lever:** narrow the wedge to a deficit where shorter capture suffices (e.g., a single-room neglect protocol), or add a $300 paired edge-box for compute and pair with a thicker form factor for the therapy session.
2. **Assumption: rehab clinic buyers will adopt a glasses-based home program at sufficient unit volume to make the per-clinic ACV math work.**
   - **What would pressure it:** clinics tell us their patients (median age ~70 for stroke) won't wear glasses, or that the loaner-pool logistics (cleaning, returns, breakage) consume more therapist time than the program saves.
   - **Lever:** start with a younger TBI cohort where wearable adoption is non-issue, build the home-program ops with a regional partner before scaling, or pivot to in-clinic-only delivery (smaller market but no logistics).
3. **Assumption: per-patient generated therapeutic content meaningfully outperforms a generic high-quality program enough to justify the price premium and the regulatory burden.**
   - **What would pressure it:** a 12-week pilot shows no functional-outcome difference between Atelier and a well-designed generic glasses program; published transfer-of-training literature suggests environment-anchoring is a smaller effect than we project.
   - **Lever:** narrow personalization to the high-leverage axes only (e.g., environment layout for neglect, routine cues for prospective memory), reducing per-patient generation cost and shifting the price down to a margin that doesn't require an outcome lift to justify.
4. **Assumption: incumbents (MindMaze, Akili, or a new Meta Health offering) won't sprint into the per-patient-glasses-rehab tier within 24 months.**
   - **What would pressure it:** Meta announces a Health-branded developer kit for Ray-Ban / Orion glasses with reimbursement-aligned APIs.
   - **Lever:** lean harder on the patient-environment dataset moat (where the incumbents structurally don't collect data) and on the clinical-evidence publication pipeline as the procurement gate.

## 2-week experiment

**Load-bearing assumption to test:** that a 30-minute home capture on consumer-grade smart glasses produces enough spatially-anchored data to generate a *recognizably better-than-generic* spatial-neglect therapy session — and that a rehab medical director, watching the demo, will say "I would pilot this."

**Artifact to build (week 1):** a working v0 demo Vincent can build solo in 5 days using coding agents:
- Pre-recorded 30-min home capture (Vincent's own apartment, shot on a Ray-Ban Meta or an iPhone in a glasses-mount as proxy).
- A pipeline that ingests the capture, runs on-device-class models locally to extract the room layout + identify ~15 task-relevant objects (cabinets, light switches, doorways).
- A generated browser-rendered "session" — a 10-minute spatial-neglect therapy module where the patient is cued (audio + simple overlay) to attend to specific objects in the captured environment, with response logging and a clinician-facing one-page session summary auto-formatted as a cognitive-rehab progress note.
- Hosted as a 5-minute screencast + a clickable demo link for buyers who want to play with the session module on their own captured space.

**Conversations (week 2):** 6–8 outpatient rehab medical directors and lead OT/SLPs at neuro-rehab clinics in Boston, NYC, and Bay Area (cold + warm intros via Vincent's Siemens-era hospital network). Each conversation opens with the screencast, then offers them the chance to share a 5-minute capture of their own clinic gym to see the session generated for that space.

**Specific questions / asks:**
1. Watching this generated session: does it look meaningfully better than your current spatial-neglect home program, or like a more expensive version of the same thing?
2. If it cleared a 12-week functional-outcome RCT vs. standard-of-care, what price per patient would your clinic pay against existing reimbursement?
3. Who in your org needs to sign off on a paid pilot — and what's the smallest pilot (patient count, dollar value) you could greenlight without going through formal procurement?
4. What objection would your therapists raise first?

**Pass criteria:** ≥2 verbal LOIs for a paid pilot at ≥$10k AND ≥1 buyer names a specific PO date or budget line AND ≥1 clinician asks to capture their own clinic gym (engagement signal that the artifact is conversation-changing, not a polite watch).

**Kill criteria:** 0 of 8 buyers say they would pilot at any price, OR the dominant feedback is "the personalization isn't the bottleneck — adherence and reimbursement are," which would mean the wedge is wrong even if the technology works.

**Vincent's effort:** ~50 hours total. ~30h on the artifact (capture, pipeline, session module, screencast). ~20h on outreach and conversations. Output: hosted demo + memo with quoted answers + go/pivot/kill recommendation.

## What we don't know yet

- Whether the patient cohort (median stroke age ~70) will tolerate hour-a-day glasses wear at home for 12 weeks, beyond the early-adopter TBI subset.
- Whether on-device generation quality on Ray-Ban-class hardware (versus Orion-class) is good enough today, or whether the bet pulls forward by 12–24 months.
- The realistic time-to-FDA path for a per-patient-generated therapeutic device (precedent is thin: Akili's EndeavorRx took ~7 years from start to FDA authorization).
- Whether the strongest GTM is direct-to-clinic, partnered with a rehab software incumbent (Net Health, WebPT), or partnered with a glasses OEM's emerging health programs.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses]] — adjacent: also smart-glasses-in-clinical-workflow, but Sterile's buyer is the CMO and the user is the clinician (documentation), not the patient (therapy).
- [[Tessera — Fit-confidence API for agent-mediated apparel commerce trained on smart-glasses body capture]] — methodological cousin: the "use the user's own kept artifacts as the revealed-preference signal" pattern, applied here to the patient's own home environment instead of their wardrobe.
