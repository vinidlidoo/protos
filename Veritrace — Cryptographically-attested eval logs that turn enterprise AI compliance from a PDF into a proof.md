---
proto_generator:
  seed: 420631118
  writer: 1
  writers_total: 2
  repo_sha: 0a63ec4
  generated_at: 2026-04-28T23:30:26+00:00
id: proto-veritrace
aliases:
  - Veritrace
tags:
  - proto
type: proto
status: passed
created: 2026-04-28
origin: ""
---
# Veritrace — Cryptographically-attested eval logs that turn enterprise AI compliance from a PDF into a proof

## What is it?

**Elevator pitch**: Veritrace is a sidecar that sits next to a regulated enterprise's AI workflows (think a bank's claims-triage agent, an HR vendor's CV screener) and emits a tamper-evident, machine-checkable log of every inference: which model ran, what eval scores it produced against the customer's own benchmark, what data class went in, and a hardware attestation that the recorded run is the run that actually happened. Auditors and regulators stop accepting marketing PDFs and start verifying signed evidence in seconds.

**How it works**: The customer wraps their model endpoint (OpenAI, Anthropic, in-house) with our SDK or runs our enclave-deployed gateway. Each call produces (a) a content-addressed record of inputs/outputs (or hashes thereof, when raw content can't leave), (b) eval scores computed on-the-fly by a customer-defined eval suite — hallucination, PII leakage, jurisdictional carve-outs — and (c) a remote-attestation quote from the TEE that ran the eval, signed by Intel TDX / AMD SEV-SNP / NVIDIA Confidential Compute keys. The bundle is anchored periodically via a Merkle root and made available to the customer's auditors through a verifier they can run locally. Value compounds because the audit artefact becomes the **deployment unit** — every new model version, every new jurisdiction, every new agent tool requires a fresh attested baseline, and Veritrace owns that pipeline.

## Why now (2026)

- **The EU AI Act's high-risk obligations bind on 2 August 2026**, requiring "logging of activity to ensure traceability of results" and post-market monitoring for any AI system in the high-risk Annex III categories (credit, hiring, biometrics, critical infra) ([European Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). Non-compliance with high-risk obligations carries administrative fines up to €15M or 3% of global turnover, whichever is higher, under Article 99 ([AI Act Article 99](https://artificialintelligenceact.eu/article/99/)).
- **Realistic compliance lead time is 32–56 weeks** per Modulos's 2025 readiness analysis — meaning enterprises that haven't started by mid-2026 are already late, and every quarter that slips raises the willingness to pay for any tool that converts narrative compliance into automated evidence ([Modulos](https://www.modulos.ai/blog/eu-ai-act-high-risk-compliance-deadline-2026/)).
- **TEE-backed inference is now hardware-real, not academic**: NVIDIA's Hopper and Blackwell platforms ship a Remote Attestation Service that issues cryptographic proof a workload ran inside a verified enclave on a verified GPU — the missing primitive for binding eval results to physical execution ([NVIDIA](https://www.nvidia.com/en-us/data-center/solutions/confidential-computing/)).
- **zkML for transformer-class inference crossed the practicality line in 2024–25**: zkLLM proved a 13B-parameter forward pass in <15 minutes with a <200KB proof at ACM CCS 2024, and EZKL ships a production toolchain converting any ONNX model into a Halo2 zk circuit ([zkLLM paper](https://arxiv.org/abs/2404.16109), [EZKL repo](https://github.com/zkonduit/ezkl)). Not yet fast enough for per-call zk proofs on GPT-4 class models, but already adequate for *eval circuits* (small classifier models scoring outputs) — which is the part you want cryptographically bound.
- **Governance platforms are exploding but they govern policy, not execution**: Credo AI was named #6 in Applied AI on Fast Company's 2026 most-innovative list and shipped EU AI Act policy packs, yet its evidence layer remains "automated evidence generation" of *workflow attestations* — a compliance officer ticking boxes inside a SaaS, not a cryptographic proof a regulator can verify offline ([Credo AI](https://www.credo.ai/product)).
- **Privacy concerns around enterprise AI are compounding silently**: every CISO assumes a megaphone-level breach of AI transcripts is coming; once it lands, "we have a SOC 2 from our vendor" stops being an acceptable answer overnight. Veritrace is the answer that survives that news cycle.

## Who else is doing this

- **AI governance platforms (policy-layer)** — leader: **[Credo AI](https://www.credo.ai/product)**. Others: [Holistic AI](https://www.holisticai.com/), [Modulos](https://www.modulos.ai/), [FairNow](https://fairnow.ai/). They govern policies and produce workflow-style audit logs but don't bind execution to hardware. A regulator must trust the platform's word that what's logged matches what ran.
- **LLM eval / observability** — leaders: **[Arize](https://arize.com/)**, [Patronus AI](https://www.patronus.ai/), [Braintrust](https://www.braintrust.dev/), [LangSmith](https://www.langchain.com/langsmith). Strong eval primitives and traces, no cryptographic attestation, no compliance-grade evidence — explicitly an internal observability play.
- **Confidential AI / TEE infrastructure** — leader: **[Fortanix Confidential AI](https://www.fortanix.com/platform/confidential-ai)**. Others: [Anjuna](https://www.anjuna.io/), [Edgeless Systems](https://www.edgeless.systems/), [iExec](https://www.iex.ec/). Provide secure enclaves and remote attestation; treat eval as out of scope. Customer still has to glue eval results to attestations themselves.
- **Compliance automation (general purpose)** — leaders: **[Vanta](https://www.vanta.com/)**, [Drata](https://drata.com/), [Secureframe](https://secureframe.com/). Crushing SOC 2 / ISO 27001, beginning to ship AI-specific frameworks, but evidence is screenshots and integration pulls — same trust-the-vendor model as governance platforms.
- **zkML toolchains** — **[EZKL](https://github.com/zkonduit/ezkl)**, [Modulus Labs](https://www.modulus.xyz/), [Giza](https://www.gizatech.xyz/). Pure cryptography plays aimed mostly at on-chain verifiable agents in DeFi. No enterprise compliance distribution, no eval framework, no buyer relationships in regulated industries.

**Where the opening is**: every adjacent category solves one of three problems — *what should be logged* (governance), *how good was the output* (eval), *did this code really run on this hardware* (TEE / zk). Nobody binds the three into a single artefact a regulator can verify without trusting the vendor. Incumbents won't naturally close it: Credo's customers don't want to switch eval pipelines; Arize doesn't sell to compliance officers; Fortanix sells to platform engineers; the zkML crowd sells to crypto. The wedge is the enterprise compliance buyer who already has eval scripts and an inference stack, and just needs the evidence layer that turns both into something legally defensible. That buyer exists in every Annex III enterprise from August 2026 onward.

## Why us

- **Vincent's two years leading AI model evaluations at Amazon are direct, scarce experience in how a Fortune-500 measures AI quality, regression, and risk at production scale** — knowledge that maps 1:1 to the eval layer of Veritrace, and that a pure-cryptography or pure-compliance founder would take years to acquire. The buyer profile (compliance officer + ML lead + procurement) is people Vincent has already sat across the table from.
- **Active multi-part ZK study published in 2025–26 means Vincent can credibly architect the cryptographic layer himself** rather than hiring a specialist before product-market fit. This compresses the discovery loop: he can prototype the attestation pipeline end-to-end with coding agents, and speak fluently to both auditors and zk researchers — a combination essentially nobody else in the eval-tooling space has.

## Customer & buyer

- **Customer**: ML platform lead or AI governance lead at a regulated enterprise (bank, insurer, large healthcare system) or at a B2B AI vendor selling into them (HR-tech, claims-tech, lending).
- **Buyer**: Chief Compliance Officer or VP Risk; budget line is "AI risk / regulatory tooling," typically already funded by the AI-Act provision in the FY26 budget. Initial ACV target $80–150K, expanding to $250–500K after model count grows.
- **Champion**: the ML platform lead — the person currently being asked to produce evidence for the auditor and shipping homemade scripts. Veritrace makes them the hero who automated the audit prep.
- **ICP test**: ≥1 production AI system in an EU Annex III category OR a US sector regulator (NYDFS, OCC, FDA SaMD) explicitly asking for model documentation; ≥3 model versions in production; CCO has either commissioned an external audit or has one scheduled within 12 months.
- **Anti-customer**: pre-product-market-fit AI startups, anyone whose AI doesn't touch a regulated decision, and large clouds' internal teams (they'll build their own).

## Wedge / where we could enter

- **Candidate A — EU-Act audit evidence pack for B2B AI vendors selling into European banks**. Narrow, time-boxed by the August 2026 deadline. The vendor uses Veritrace to hand each banking customer a signed evidence bundle satisfying the deployer's Article 26 obligations. Pull-based: their customers ask for it.
- **Candidate B — Hallucination-attested medical scribe layer**. Sit behind Abridge / Suki / Nuance-style scribes; produce a per-encounter attestation that hallucination evals ran and passed thresholds, signed for the clinic's malpractice carrier. Higher technical lift but a single insurer-side champion can pull dozens of clinics in.
- **Candidate C — Model-card-as-a-proof for foundation-model resellers / AI marketplaces**. Each model on a marketplace ships with a Veritrace evidence pack the buyer can verify before integrating.

Push toward Candidate A first: shortest sales cycle (regulatory deadline does the closing), smallest technical surface (one eval class — PII / jurisdictional carve-outs — covers most early demand), and the buyer is already actively looking. B and C become viable expansions once A produces 10+ logos.

## What makes it defensible

- **(a) Primary — proprietary eval circuit library**: a catalogue of zk-friendly small models that score the outputs of large models (PII detection, hallucination, jurisdictional compliance, specific bias tests). Each circuit takes engineering work and regulator-side validation. After 18 months we have the largest tested catalogue and every new customer expands it; switching cost grows with each one.
- **(b) Secondary — auditor / regulator network effects**: once a Big Four auditor accepts a Veritrace evidence pack as satisfying part of an AI-Act conformity assessment, every other auditor wants compatibility. We become the de-facto file format. Replicating requires the years of regulatory relationship-building, not code.
- **(c) Year-3 endgame — the trust root for a marketplace of attested AI agents**: as agentic systems compose tools across companies, only attested inference can be safely chained. Veritrace becomes the equivalent of "TLS for agent-to-agent trust" — boring, infrastructural, and embedded everywhere.

## How it could make money

| Layer                             | Price range        | Comparable                                                                                |
| --------------------------------- | ------------------ | ----------------------------------------------------------------------------------------- |
| **Per-customer subscription**     | $80K–250K / year   | [Vanta](https://www.vanta.com/pricing) Enterprise tier (custom, on-request)               |
| **Per-attested-call metering**    | $0.001–0.01 / call | [NVIDIA Remote Attestation Service](https://docs.nvidia.com/attestation/index.html) — usage-based attestation primitive |
| **Auditor / regulator licensing** | $50K–150K / year   | [Credo AI](https://www.credo.ai/product) governance-platform enterprise tier              |

Honest caveat: the obvious model-risk is **services-trap**. The first 5 enterprise deployments will require heavy hand-holding to wire eval circuits into their model stack and to walk auditors through the verifier — easily 30–50% of revenue in services for year 1. The discipline is to productise every services hour into the next customer's onboarding, and to refuse customers whose eval needs are so bespoke they can't be templated within 90 days.

## What would pressure the thesis

1. **Assumption**: Regulators and auditors will accept cryptographic attestations as superior evidence to today's PDF-and-screenshots approach.
   - **What would pressure it**: the EU AI Office's harmonised technical standards (due 2026–27) explicitly enshrine traditional documentation patterns and don't allow credit for cryptographic evidence; or auditors openly say "we don't know how to verify this so we'll keep asking for the PDFs anyway."
   - **Lever**: ship the verifier as a Big Four–co-branded tool from day one (paid pilot with one of them) so the evidence format is the auditor's native format, not ours.
2. **Assumption**: The EU AI Act's August 2026 deadline holds and is enforced with material penalties within 12 months.
   - **What would pressure it**: the November 2025 Commission proposal to slip the high-risk deadline to 2027 actually passes, or enforcement is delegated to member-state regulators who go soft for the first two years.
   - **Lever**: pivot the wedge to NYDFS / OCC model risk (SR 11-7 + the 2024 AI guidance) and FDA SaMD where the regulatory clock is independent of the EU.
3. **Assumption**: zkML / TEE attestation is fast and cheap enough for production AI workloads at the eval layer (we don't need to prove the LLM, only the eval).
   - **What would pressure it**: customers demand attestation of the LLM itself, where today's zkLLM is still 15-min-per-inference; or TEE GPUs stay supply-constrained / 30%+ price premium through 2027.
   - **Lever**: degrade gracefully — offer "TEE-only" tier (no zk) for cost-sensitive customers; reserve zk-attested eval for the highest-risk decisions where customers will pay 10× per call.

## 2-week experiment

**Load-bearing assumption to test**: a regulated-industry compliance buyer will pay for cryptographic eval-bound attestations *now* (ie. signs an LOI before the August 2026 deadline) rather than dismiss them as over-engineered relative to a "good enough" Credo-style governance product.

**Artifact to build (week 1)**: a working v0 of Veritrace — a Python/TypeScript SDK that wraps a model call (OpenAI / Anthropic), runs a configurable eval (start with a simple PII-leakage detector and a hallucination grader), executes the eval inside an Intel TDX or NVIDIA H100-CC enclave on a public cloud, and emits a signed JSON bundle (model hash, input hash, output hash, eval scores, attestation quote, Merkle root). Plus a 2-page sample evidence pack rendered as a PDF for a fictional Annex III use case ("AI-driven CV screener used by a Tier-2 European bank"), and a companion 5-minute Loom showing an "auditor" (Vincent, in a different shirt) verifying the bundle locally with a single CLI command. All code public on GitHub under a permissive license — OSS-as-table-stakes is increasingly the default and accelerates trust with a security/compliance audience.

**Conversations (week 2)**: 8–12 conversations with named segments, artifact in front of the buyer, not a deck:
- 4 with Heads of AI Risk / Compliance at European banks or insurers (warm intros via Vincent's Amazon network and ZK-study readership).
- 3 with B2B AI vendors selling into EU regulated buyers (HR-tech, lending, insurance — these are the deployers asking *their* vendors for evidence).
- 2 with Big Four AI assurance partners (PwC, EY, Deloitte, KPMG) — they hold the buy-side leverage.
- 1–2 with security/compliance-focused VCs who back this category for outside-in calibration.

**Specific questions / asks** (the ones answerable in 30 minutes with the artifact open):
1. "Show me the audit pack you produced for your last AI-system review — could this replace it, augment it, or is it solving a problem you don't yet have?"
2. "If we shipped this to your auditor, would they know what to do with it? Who's the one human in your audit firm who would?"
3. "What's your current FY26 budget line for AI compliance tooling, and what's the largest single tool inside it?"
4. "Would you sign an LOI for $X to be a design partner with a Q4 2026 deployment date, conditional on Big Four–verifier compatibility?"

**Pass criteria**: ≥3 design-partner LOIs (any size) AND ≥1 buyer commits a PO date within 6 months AND the public GitHub repo gets ≥150 stars or ≥5 inbound enterprise-buyer DMs within 14 days of launch.

**Kill criteria**: 0 LOIs after 12 conversations AND auditors uniformly say "we wouldn't know how to use this." If only one of the two fails, iterate the wedge (eg. switch from EU AI Act to US SR 11-7) and rerun a 2-week sprint.

**Vincent's effort**: ~70 hours total. ~45 hours build (TEE setup is the longest pole; coding agents handle the SDK and PDF generator), ~25 hours conversations + memo. Output: linked GitHub repo, hosted demo, the signed sample evidence pack, a Loom walkthrough, and a memo of quoted answers + a go / pivot / kill recommendation.

## What we don't know yet

- Whether auditors will treat a cryptographic attestation as *primary* evidence or merely *corroborating* — the difference determines whether Veritrace replaces a $250K audit engagement or adds $80K to it.
- Whether the right wedge is the AI vendor (sells into 50 banks, one Veritrace deal pulls many) or the bank itself (bigger ACV, longer sales cycle).
- Whether the eval-circuit catalogue is best built in-house, crowdsourced, or licensed from existing eval vendors (Patronus / Arize partnership vs. competition).
- How fast NVIDIA Confidential Compute supply scales in 2026–27 — gates per-call cost and whether Layer-2 metered pricing is viable from day one.
- Whether the Japanese regulatory environment (FSA's evolving AI guidance) presents a parallel beachhead Vincent could uniquely access via his Japan network.

## Vincent's Feedback

- Passed 2026-04-29 after walk-through.
- Same regulation-as-primary-demand-engine problem as Foreman. Three of six "why now" bullets are regulation (EU AI Act Article 12, fines, Modulos 32–56-week lead-time framing); Wedge A is "EU-Act audit evidence pack"; the buyer is CCO/VP Risk paying out of "AI risk / regulatory tooling"; defensibility leans on auditor/regulator network effects. I'm not motivated by businesses that run on regulatory pull I don't think delivers meaningful value to the underlying customer.
- Tried to pitch this without the regulator angle — "eval-evidence as a B2B AI sales accelerator," "trust primitive for AI marketplaces," "TLS for agent-to-agent commerce," "internal CISO/risk." None stuck.
- The deeper reason none stuck — and the sharpest point of the walk-through — is that the customer's actual blocker in B2B AI sales is **eval validity**, not eval honesty. Customers don't worry that vendors are obfuscating eval scores; if a vendor did, the customer would feel it in production within weeks and the vendor would lose them. The real worry is *does this vendor's eval suite predict whether their AI will satisfy my workload, with my edge cases, my error tolerances?* That is a domain-understanding + eval-engineering problem. Cryptographic attestation cannot move it.
- So Veritrace's primitive is well-matched to a regulator's concern (forensic evidence after an incident: "did this eval execute as claimed") and structurally mismatched to a customer's concern (predictive validity of the eval). The crypto solves the easy 10% of the trust problem while the hard 90% isn't a crypto problem.
- "Why us" was sharper here than for Foreman — AI-evals at Amazon + ZK study mapped directly onto the technical core. Doesn't change the verdict; the technical fit doesn't manufacture demand that isn't there.
- Verdict: regulation-driven version fails motivation test; non-regulation version fails because cryptographic execution-attestation doesn't address the binding customer concern (eval-to-reality fit). Pass.

## References

- [A Survey of Zero-Knowledge Proof Based Verifiable Machine Learning](https://arxiv.org/abs/2502.18535) — landscape of zkML for verifiable training, testing, and inference; useful for situating Veritrace's eval-attestation approach against the broader research direction.
- [Red Hat: Enhancing AI inference security with confidential computing](https://next.redhat.com/2025/10/23/enhancing-ai-inference-security-with-confidential-computing-a-path-to-private-data-inference-with-proprietary-llms/) — clean explainer of TEE-based AI inference for an enterprise audience; the kind of framing we'd echo in customer-facing material.

## Related

- [[Protos/Whisper — ZK attestation layer for agent-to-API calls so agents prove eligibility without leaking PII]] — sibling proto on the agent-to-agent trust angle; potential merge or sequencing decision.
- [[Protos/Bellwether — private on-prem eval harness for enterprise coding-agent fleets]] — sibling proto: same eval-platform thesis, different surface (coding agents vs. regulated AI). Veritrace adds the cryptographic-attestation layer Bellwether assumes away.
