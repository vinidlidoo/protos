---
id: proto-sterile
aliases:
  - Sterile
tags:
  - proto
type: proto
status: drafted
created: 2026-04-28
origin: ""
proto_generator:
  seed: 400633033
  writer: 1
  writers_total: 2
  repo_sha: 2a1d25c
  generated_at: 2026-04-28T21:44:01+00:00
---

# Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses

## What is it?

**Elevator pitch.** Sterile is a HIPAA-compliant capture, redaction, and EHR-integration layer that lets surgeons and proceduralists wear consumer smart glasses (Ray-Ban Meta Display, Apple, Samsung XR) inside the OR and procedure suite without violating patient privacy. Hospitals pay a per-glasses subscription; surgeons get hands-free photo/video documentation, first-person teaching streams, and a structured procedure note in the EHR — all routed through an in-hospital appliance that strips PHI before anything leaves the building.

**How it works.** A clinician wears a paired-and-locked consumer glasses unit (Meta is shipping the Ray-Ban Display + Neural Band at $799 — a price point a department can buy 20 of, not 2 [Meta announcement](https://about.fb.com/news/2025/09/meta-ray-ban-display-ai-glasses-emg-wristband/)). All capture is intercepted by Sterile's mobile app + on-prem appliance: faces and identifiers are redacted from photos/video on-device, audio is transcribed locally and never reaches Meta's cloud, and the cleaned artifact is written to the procedure record with the right CPT/HCPCS metadata. A second product surface — a teaching stream — lets a remote attending or fellow watch the surgeon's POV with PHI stripped in real time, replacing the awkward "phone-on-tripod" telementoring that hospitals do today. Where the value compounds: every procedure builds a redaction library and a structured procedure-note dataset that the audio-only ambient scribes (Abridge, DAX, Suki) cannot generate because they never see the wound.

## Why now (2026)

- **The hardware just crossed the line.** Meta shipped the Ray-Ban Display + Neural Band on September 30, 2025 at $799 — a true-display, EMG-controlled, prescription-compatible glasses unit, not just a camera with speakers [Meta announcement](https://about.fb.com/news/2025/09/meta-ray-ban-display-ai-glasses-emg-wristband/). Apple, Samsung, and Google are racing into the same form factor in 2026–2027. Clinical-grade hardware (Vuzix M400, HoloLens) has stalled — Microsoft ended HoloLens 2 production — so the mainstream is now consumer.
- **Surgeons are already using consumer glasses informally.** A peer-reviewed study (Nov 2023–Apr 2025) put Ray-Ban Meta into foot-and-ankle limb-preservation surgery for hands-free intraoperative photo, video, and remote consultation; trainees preferred the first-person stream over conventional video [PubMed 41045069](https://pubmed.ncbi.nlm.nih.gov/41045069/). This is happening with no compliance layer.
- **Hospitals are starting to ban them — explicitly because there's no BAA path.** Meta does not sign Business Associate Agreements, glasses upload audio/video to Meta's cloud and train models by default, and the devices "bypass IT governance entirely" [LBMC analysis](https://www.lbmc.com/blog/meta-rayban-smart-glasses-hospital-ban/). Hospital CISOs are stuck choosing between "ban" and "ignore" — there is no third option. Sterile is the third option.
- **Ambient scribe is a $1B+ category and has saturated the audio surface.** Abridge won #1 Best in KLAS 2026 for the second straight year [Abridge](https://www.abridge.com/best-in-klas-2026); WVU Medicine deployed it to 2,800 clinicians across 25 hospitals [HIT Consultant](https://hitconsultant.net/2026/03/11/wvu-medicine-expands-abridge-ai-ambient-scribe-rural-healthcare/). But every winner is microphone-based and built for the exam room. Procedural specialties (surgery, cath lab, endoscopy, IR, dermatology procedures) are unaddressed because the eyes are on the wound.
- **Epic shipped its own ambient scribe in early 2026, compressing margins for audio-only startups** [MedCity News](https://medcitynews.com/2026/02/ambient-scribe-ai-startups-epic/). The defensible niches for the next wave are subspecialty + new sensor modality. Procedural-glasses is both.
- **EU AI Act high-risk obligations land August 2, 2026** as the original baseline for AI in medical devices; the proposed Digital Omnibus extension would push embedded-AI obligations (medical devices included) to August 2, 2028 [MedDeviceGuide](https://meddeviceguide.com/blog/eu-ai-act-medical-devices-compliance-guide). Either way, hospitals shopping for AI-glasses tooling will need vendors who already speak conformity-assessment language — a moat that favors a focused vertical player over a consumer hardware OEM.

## Who else is doing this

- **Ambient AI scribes (audio-only, exam-room).** Market leader: **[Abridge](https://www.abridge.com/best-in-klas-2026)**. Others: [Microsoft DAX Copilot](https://www.microsoft.com/en-us/industry/blog/healthcare/2024/08/08/dax-copilot-new-customization-options-and-ai-capabilities-for-even-greater-productivity/), [Suki / Abridge / DAX pricing comparison](https://www.commure.com/blog-scribe/scribe-pricing), [Ambience Healthcare](https://medcitynews.com/2025/07/healthcare-documentation-startup-unicorn/) ($243M Series C, $1.25B valuation), [Augmedix](https://www.augmedix.com/) (now part of Commure). All built around a microphone capturing a clinic conversation. None see the procedure or work hands-free with sterile fields.
- **Industrial smart-glasses platforms reaching toward healthcare.** Main player: **[Vuzix M400](https://www.vuzix.com/pages/healthcare)** (HIPAA-positioned, IEC60601-certified, but ~$2k+ industrial unit, no scribe AI, no Meta-style consumer comfort). Others: [RealWear Navigator Z1](https://www.realwear.com/) (industrial-frontline focus, not healthcare). These are good hardware looking for software; Sterile is software-on-consumer-hardware that scales with Meta/Apple's R&D budget instead of fighting it.
- **Surgical AR / pre-op planning.** Main player: **[Medacta NextAR](https://nextar.medacta.com/)** (FDA-cleared for total knee arthroplasty, August 2020 — see [Healio coverage](https://www.healio.com/news/orthopedics/20200821/medacta-receives-fda-clearance-for-augmented-realitybased-tka-platform); shoulder application has since received FDA clearance, spine application is CE-marked). These are Class II SaMD focused on intraoperative *guidance*, not capture/scribe. Sterile's wedge is workflow + compliance, not surgical decision support — a different regulatory posture.
- **Hospital-side compliance tooling.** Main player: **[Imprivata](https://www.imprivata.com/)** (clinical identity, mobile device endpoints). Others: existing MDM stacks. They govern devices but have no glasses-specific PHI redaction or procedure-note pipeline; Sterile would integrate with them, not replace them.

**Where the opening is.** Audio-scribe leaders cannot pivot into procedural specialties without a sensor leap they're not built for, and Meta/Apple/Samsung will not chase HIPAA/MDR conformity for a single vertical when the consumer market is 1000× larger. Industrial glasses vendors lack the EHR + clinical-AI software depth. Surgical AR vendors are focused on FDA Class II guidance, not the boring-but-essential compliance plumbing that lets a department buy 20 pairs of Ray-Bans tomorrow. The opening is a vertical software company that turns consumer glasses into a clinical-grade workflow tool — close enough to the OEMs to ride their hardware curve, close enough to the hospital to handle the BAA, the redaction, the EHR write-back, and the AI Act paperwork.

## Why us

- **Hospital and lab buyer fluency that almost no SF founder has.** 4 years at Siemens Healthineers across technical sales for medical imaging, CRM, and marketing means I've sat in radiology departments, cath labs, and procurement reviews — I know which title in the org chart actually signs, which committee delays a deal six months, and how a HIPAA + MDR compliance story is sold versus how a "productivity AI" story is sold. The audio-scribe winners had to learn this the hard way; I start there.
- **Trilingual EN/FR/JA + lived experience in three of the world's deepest hospital markets.** US, Japan, and France together account for the majority of high-margin surgical procedure volume in the developed world. Japan's hospital network specifically prizes a vendor who can sell, train, and support in-language; almost no Series A startup can do this. This compresses the international expansion timeline that usually breaks healthcare SaaS.
- **AI-coding-agent depth means a small team can ship the redaction + EHR pipeline.** The hard part of Sterile is not novel ML — it is plumbing (PHI detection, BAA-clean storage, FHIR write-back, glasses SDK integration). A founder who builds with coding agents end-to-end can compress the v0 to weeks instead of quarters.

## Customer & buyer

- **Customer:** procedural physicians — surgeons (orthopedics, podiatry, plastics, dermatology), interventional radiologists, cath-lab cardiologists, gastroenterologists. They feel the pain and want the glasses; they generate the demand.
- **Buyer:** Hospital CIO + Chief Medical Information Officer (CMIO) jointly. Budget line: clinical IT / digital transformation, often with co-funding from a service-line P&L (e.g., orthopedic surgery department) once volume is proven. Typical ACV: **$80–$250k year 1** for a 25–60-glasses department deployment.
- **Champion:** a procedural service-line chief or medical director of perioperative services who is already losing residents to documentation burden and wants to differentiate the program for recruiting.
- **ICP test:** US AMC or large IDN with (a) ≥1 procedural service line that already attempted to use consumer glasses informally and got told to stop by IT, (b) Epic or Oracle Health on the EHR side, (c) an existing ambient-scribe contract for the clinic side that does not extend into procedures.
- **Anti-customer:** small ambulatory practices without IT staff (will not absorb the appliance), and pure-FDA-guidance plays (we are not building Class II surgical navigation; that is a different, slower regulatory road).

## Wedge / where we could enter

- **Candidate A — Surgical photo/video documentation for podiatry & orthopedic limb preservation.** The published evidence already exists; the workflow is well-defined; reimbursement for wound documentation is meaningful; departments are small enough to land in one quarter. Highest-likelihood wedge.
- **Candidate B — Telementoring for trauma and rural-hospital surgery transfer networks.** Solves a real revenue + outcomes problem (the receiving hospital wants to see the field), strong tailwind from the WVU/Abridge-style rural deployments, but the buyer is a network rather than a department.
- **Candidate C — GI endoscopy procedure capture.** High procedure volume, recurring billing, sterile-field problem is mild (no scrub barrier for the proceduralist's head), but reimbursement-tied capture (already-required photo documentation) makes it a stickier ROI story.

What pushes us toward A: the existing peer-reviewed clinical evidence and the small department size make the first 3 design partners reachable in 90 days. We start at A, with B and C as the second-year expansion targets.

## What makes it defensible

- **(a) Primary — clinical workflow integrations + BAA-grade compliance posture.** Every customer onboards a redaction model, an EHR mapping for that institution's procedure-note schema, and a signed BAA with Sterile (not with Meta). This is months of work per institution; once landed, switching cost is high and Meta cannot sell direct.
- **(b) Secondary — proprietary procedural sensor dataset.** Audio scribes have only audio. Sterile accumulates synced first-person video + audio + EMG-gesture + procedure-note labels across thousands of cases. This is the corpus needed to train procedure-aware AI (CPT inference, surgical step segmentation, complication flagging). No incumbent has it.
- **(c) Year-3 endgame — the procedural-AI platform OEMs route through.** When Apple ships its glasses and wants to enter clinical, the path of least resistance is to partner with the company that already has the BAAs, the EHR connectors, and the procedural corpus. Sterile becomes the Stripe of clinical glasses: the layer every glasses OEM and every EHR pipes through, rather than each rebuilding the compliance stack.

## How it could make money

| Layer | Price range | Comparable |
| --- | --- | --- |
| **Layer 1 — Per-clinician subscription** | $300–$600 / clinician / month | [DAX Copilot ~$600/mo per Commure](https://www.commure.com/blog-scribe/scribe-pricing); [Abridge ~$600–$800/mo enterprise per Scribing.io](https://www.scribing.io/blog/abridge-ai-scribe-cost-analysis) |
| **Layer 2 — Per-hospital appliance + department platform fee** | $40k–$120k / year | [Vuzix M400 healthcare](https://www.vuzix.com/pages/healthcare) hardware + software bundle range |
| **Layer 3 (later) — Procedural-AI add-ons (CPT capture, complication flag, telementoring minutes)** | $50–$200 / procedure | [Medacta NextAR](https://nextar.medacta.com/) per-procedure surgical AR pricing, transaction-style |

**Business-model risk.** Per-procedure pricing only works once we are tied to revenue (CPT capture that improves billing) or quality (complication detection that lowers readmit rates). Until then, Layers 1+2 are the durable revenue and Layer 3 is the upsell. The trap to avoid: getting boxed into a hardware-reseller margin on the glasses themselves — we explicitly do not resell glasses, the hospital procures them through normal channels and Sterile attaches the software wrap.

## What would pressure the thesis

1. **Assumption:** Hospital CISOs would rather adopt a compliance layer than maintain an outright ban on consumer smart glasses.
   - **What would pressure it:** ban-by-default policies harden into industry norm via JCAHO/AAMI guidance; CISOs prefer "no glasses anywhere" as a defensible posture and refuse to evaluate any wrap.
   - **Lever:** pivot to a captive-fleet model — Sterile-flashed glasses procured as a regulated medical accessory through a hospital MDM channel, marketed as "we removed Meta's cloud entirely from this device."
2. **Assumption:** Meta keeps glasses APIs open enough for a third-party redaction/capture layer to intercept media before cloud upload.
   - **What would pressure it:** Meta locks the glasses pipeline (as Apple has historically done), or Meta launches its own healthcare BAA program and goes direct.
   - **Lever:** shift hardware bet to Apple/Samsung/Google as they enter the category — the moat is the clinical workflow, not the OEM-specific SDK. Or pivot toward Vuzix/RealWear hardware partnerships if all consumer OEMs close down.
3. **Assumption:** Procedural specialties value first-person POV capture enough to pay $250–$500/mo/clinician — i.e. it clears the bar audio scribes already proved exists.
   - **What would pressure it:** surgeons treat the glasses as a nice-to-have, not a workflow critical, and adoption stalls below the 30%-of-physicians threshold that drives EHR-anchored deals.
   - **Lever:** narrow to the 2–3 specialties with explicit reimbursement-tied photo documentation requirements (wound care, dermatology lesion tracking) where the ROI is auditable in the billing system, not in clinician-satisfaction surveys.

## 2-week experiment

**Load-bearing assumption to test.** Procedural physicians (starting with podiatric surgeons doing limb preservation) will book a 30-minute call to see a working glasses-to-EHR redaction demo, and at least 3 of them will commit verbally to a paid pilot if their hospital's CISO signs off on the compliance architecture.

**Artifact to build (week 1).** A working v0 of Sterile-Demo, runnable end-to-end on Vincent's laptop:

- Pair a Ray-Ban Meta Display unit, intercept captured photo + video via the Meta companion-app developer surface
- On-device PHI redaction pipeline (face blur, OCR-then-blur for charts/labels visible in frame, audio transcription with PHI tagging)
- A redacted artifact gets posted via FHIR `DocumentReference` to a public FHIR sandbox (HAPI test server) with the right metadata fields filled in (patient pseudo-ID, encounter, procedure)
- A 90-second screencast of the full flow: surgeon-POV → on-device redact → EHR record. Hosted publicly (Loom or YouTube unlisted, sharable to CMIOs without a login wall).
- A one-page architecture diagram showing the on-prem appliance, the BAA boundary, and what data does and does not leave the building.

**Conversations (week 2).** 12 procedural physicians + 3 hospital CMIOs. Targeting:

- 6 podiatric and orthopedic limb-preservation surgeons sourced from authors of the existing Ray-Ban Meta surgical literature [PubMed 41045069](https://pubmed.ncbi.nlm.nih.gov/41045069/) and the AAOS member directory.
- 6 GI/IR proceduralists (warm-list reachable through Vincent's Siemens Healthineers network).
- 3 CMIOs at AMCs known to be Epic-anchored and ambient-scribe customers.

Each call opens by sending the screencast 24h prior and the architecture diagram 1h prior; the call itself is "show me your reaction, then 6 questions."

**Specific questions / asks.** Each ≤30 minutes, asked while the artifact is on-screen:

1. Would your IT department let this device into the OR if Sterile signed a BAA? Yes / no / "depends on" (record the specific blockers).
2. What does the procedure-note workflow look like today, and where would this slot in?
3. Whose budget pays — clinical IT, the surgical service line, perioperative services, or somewhere else?
4. What price per clinician per month would your department absorb without a finance committee review?
5. If we offered you a 90-day free pilot for 5 clinicians, who at your institution would you need to bring along to say yes?
6. Where would this fail? What is the most likely reason you'd cancel after 60 days?

**Pass criteria.**

- ≥3 verbal commitments to a paid pilot conditional on hospital sign-off (LOIs preferred but not required for pass)
- ≥1 CMIO confirms a path to BAA + procurement within 6 months and names the next two meetings
- The artifact (screencast + architecture diagram) gets ≥500 views or ≥10 inbound replies from clinical accounts when posted to LinkedIn / clinical Twitter / Bluesky

**Kill criteria.**

- 0 paid-pilot commitments after 12 procedural physician conversations
- All 3 CMIOs say "we will not allow consumer glasses in the OR under any wrap" — this would mean Lever 1 from the thesis-pressure section is needed, which is a different (and slower) bet
- Meta ships an official healthcare-BAA program covering this use case in the 2-week window — the moat collapses

**Vincent's effort.** ~70 hours over 2 weeks. ~40 hours building the artifact (week 1, mostly directing coding agents on the pipeline and the FHIR write-back), ~30 hours conversations + writeup (week 2). Output: hosted screencast + architecture diagram + memo with quoted answers + go / pivot / kill recommendation.

## What we don't know yet

- What does the Meta Ray-Ban Display developer surface actually expose? Can a third party intercept media before cloud upload, or does that require a private partnership with Meta?
- How does the FDA classify a redaction-and-routing layer that does not generate clinical recommendations? Likely not Class II SaMD, but worth a regulatory consult before the demo conversations.
- Which is the highest-volume EU-equivalent jurisdiction for a year-2 launch — France (Vincent's network, slower procurement) or Japan (Vincent's network, faster pilot but stricter privacy law)?
- What is the right relationship to Apple's forthcoming glasses, given that Apple typically refuses third-party background access? Do we need a parallel Apple-only product, or can we ride Meta + Samsung + Google for the first 3 years?

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## References

- [Meta Ray-Ban Display + Neural Band launch announcement](https://about.fb.com/news/2025/09/meta-ray-ban-display-ai-glasses-emg-wristband/) — the hardware enabler that makes this bet possible in 2026 vs. 2028.
- [Ray-Ban Meta in foot/ankle surgery — peer-reviewed study](https://pubmed.ncbi.nlm.nih.gov/41045069/) — the clinical evidence that surgeons are already trying to use these and finding value.
- [LBMC — why hospitals should ban Ray-Ban Meta](https://www.lbmc.com/blog/meta-rayban-smart-glasses-hospital-ban/) — the precise compliance gap Sterile fills.
- [Commure — AI scribe pricing comparison](https://www.commure.com/blog-scribe/scribe-pricing) — anchor for Layer 1 pricing range.
- [Abridge #1 Best in KLAS 2026](https://www.abridge.com/best-in-klas-2026) — confirms ambient-scribe category maturity and the audio-only ceiling.
- [MedCity News — Epic launches its own ambient scribe](https://medcitynews.com/2026/02/ambient-scribe-ai-startups-epic/) — why audio-scribe startups are looking for new wedges.
- [EU AI Act medical device compliance timeline](https://meddeviceguide.com/blog/eu-ai-act-medical-devices-compliance-guide) — the regulatory clock that favors a focused vertical player.

## Related

- [[Protos/Polyglot — Multilingual Voice Agent Quality]] (deleted sibling — also leveraged trilingual + healthcare buyer fluency, different sensor)
