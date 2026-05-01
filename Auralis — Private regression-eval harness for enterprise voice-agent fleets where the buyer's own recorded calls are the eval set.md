---
proto_generator:
  seed: 7734679
  writer: 3
  writers_total: 3
  repo_sha: aba8ddf
  generated_at: 2026-05-01T06:03:27+00:00
id: proto-auralis
aliases:
  - Auralis
tags:
  - proto
type: proto
status: passed
created: 2026-05-01
origin: ""
---
# Auralis — Private regression-eval harness for enterprise voice-agent fleets where the buyer's own recorded calls are the eval set

> **Vault adjacency note.** [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]] takes the same private-eval pattern into *coding* agents. Auralis is a different bet: different buyer (Head of Voice CX, not Head of Developer Productivity), different eval primitives (audio + CRM dispositions, not diffs and tests), different incumbent landscape (Cresta / Observe.AI / Hamming, not Braintrust / LangSmith). The two could ship from the same shop but they are not the same wedge.

## What is it?

**Elevator pitch.** Auralis is a private regression-eval service for enterprises that have rolled out voice AI agents (collections, healthcare scheduling, claims, support) at meaningful volume. We give the Head of Voice CX a weekly scorecard that says *what got worse* on their own production calls when a vendor pushes a model upgrade, when a prompt template changes, or when the team swaps STT or TTS providers — built from the buyer's own recorded calls and CRM dispositions, never on a public benchmark.

**How it works.** A voice CX team installs an Auralis sidecar inside their VPC that taps the call recorder (Five9, Genesys Cloud, NICE, Amazon Connect, LiveKit, Pipecat). For each new candidate config, Auralis selects a stratified sample of the buyer's last 90 days of recorded calls, replays each call's caller-side audio against the candidate agent, scores the resulting conversation on five layers (ASR entity accuracy on the buyer's named-entity dictionary, intent/disposition match against the CRM ground truth, hallucination rate per AssemblyAI's "five-or-more consecutive errors" definition, latency p95, and policy-gate adherence), and ships a private weekly diff. The reference labels are the dispositions human reps actually wrote in Salesforce / Epic / the CCaaS — a revealed-preference signal the buyer already owns and that no incumbent vendor sees in full. Nothing leaves the customer's environment; the audio, the dispositions, and the eval models stay inside.

## What's the problem?

A voice CX leader running a Decagon, Sierra, Cresta, or in-house voice agent at scale has no rigorous answer when their CFO asks "should we switch the underlying model and save 70%?", or when their COO asks "did Tuesday's prompt change make CSAT worse?" Today they sample ~3% of calls manually for QA, run synthetic tests against scripts that don't reflect their real callers, and rely on lagging weekly CSAT — which arrives five days after a regression has already churned customers. Cross-vendor comparisons on their *own* call distribution are not a button anyone offers; the vendors that own the calls (Cresta, Observe.AI) cannot benchmark themselves fairly against rivals.

## Why now (2026)

- **Voice AI in enterprise contact centers crossed from pilot to production in 2025-2026.** Decagon announced a $250M Series D at a $4.5B valuation on January 28, 2026, on the heels of "more than 100 new global enterprise customers" — including Avis Budget Group, Block, and Deutsche Telekom — joining in the prior fiscal year ([Decagon Series D announcement, Jan 28 2026](https://decagon.ai/blog/series-d-announcement)). On Decagon's customer wall, Chime, Duolingo, ClassPass, and Hunter Douglas show deflection rates of 70-95% on production voice and chat ([Decagon customer case studies](https://decagon.ai/)). Sierra customers include Rocket Mortgage, SoFi, SiriusXM, Sutter Health, ADT, Sonos, and CLEAR ([Sierra customer wall](https://sierra.ai/)).
- **The voice-vs-text capability gap means voice agents need more eval, not less.** The Sierra-extended τ-Voice benchmark shows the best production voice agent scoring 51% task completion under clean audio and 38% under realistic audio (15 dB SNR background noise, accents, interruptions), versus 85% for an equivalent text agent on identical tasks — a 47-point realistic-conditions gap, with authentication transcription errors and silent hallucination (verbal task confirmation with no tool call) as the dominant failure modes ([τ-Voice benchmark analysis, Arun Baby, 2026](https://www.arunbaby.com/speech-tech/0066-tau-voice-benchmark-full-duplex-voice-agents/), [Sierra τ³-Bench announcement](https://sierra.ai/blog/bench-advancing-agent-benchmarking-to-knowledge-and-voice)).
- **Gartner's $80B / 1-in-10-calls forecast set the buying motion in motion.** Gartner predicts conversational AI will reduce contact-center agent labor costs by $80B in 2026 and automate 1-in-10 agent interactions (vs. 1.6% today), with the forecast specifically calling out 2,500+ agent operations as the lead-adopter segment ([CX Today coverage of the Gartner press release](https://www.cxtoday.com/workforce-engagement-management/gartner-bots-cut-agent-labor-costs-80bn/)). That's the buyer Auralis sells to.
- **Voice-agent QA is now an explicit category.** Hamming raised $3.8M seed for at-scale voice-agent testing and lists customers like Smith.ai (3,500+ clients), Bland Labs, Grove AI, Podium, and Luma Health, with claims of 95-96% agreement with human evaluators on audio-native evals ([Hamming homepage](https://hamming.ai/)). The category exists; it is not yet enterprise-on-prem.
- **The horizontal LLM-eval winners (Braintrust, LangSmith, Patronus) are text-shaped, not audio-shaped.** Hamming's own metrics guide enumerates the dimensions a voice eval has to cover and that text tools don't — WER, time-to-first-word, turn latency, barge-in recovery, MOS, hallucination-under-noise — alongside business outcomes ([Voice Agent Evaluation Metrics Guide, Hamming](https://hamming.ai/resources/voice-agent-evaluation-metrics-guide)). The eval primitives are different enough that text-eval winners can't simply add a voice tab.
- **a16z's adoption data confirms support is the second-largest enterprise AI use case behind coding, by revenue, and the buyer is *already* paying for AI in the contact center.** "Decagon and Sierra have grown so quickly" is named explicitly; legal and healthcare are the leading verticals ([AI Adoption by the Numbers, a16z, April 2026](https://www.a16z.news/p/ai-adoption-by-the-numbers)).

## Who else is doing this

- **Voice-native QA / testing platforms** — leader: **[Hamming](https://hamming.ai/)**. Others: [Coval](https://www.coval.dev/), [Vapi](https://vapi.ai/) (testing primitives bundled with their orchestration), [Vellum](https://www.vellum.ai/blog/ai-voice-agent-platforms-guide). Hamming is the closest competitor on product and ships SOC 2 / HIPAA, but the default deployment is their cloud — buyers regulated enough to refuse third-party SaaS access to call audio (banks, payers, providers) currently choose to do nothing, which is the opening.
- **Real-time-guidance + post-call QA incumbents** — leader: **[Cresta](https://cresta.com/)** — published AWS Marketplace SKUs are $150K/yr for "Agent Assist for Voice — up to 100,000 call subscription" and $150K/yr for "Agent Assist for Chat — up to 125,000 chat subscription" ([Cresta Contact Center AI Platform on AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-lmdwown6xoo6q)). Others: **[Observe.AI](https://www.observe.ai/)** (350+ enterprises, customers include DoorDash, Accolade, JG Wentworth), [Balto](https://www.balto.ai/). They analyze 100% of calls but their product is *their own* AI assist on *their own* model — they will not benchmark themselves against Decagon or Sierra honestly, and their eval is post-hoc CSAT scoring, not regression-eval against candidate model swaps.
- **AI-agent vendors with their own observability** — **[Decagon](https://decagon.ai/)** ships an "Optimize" stage in their platform; **[Sierra Agent OS](https://sierra.ai/)** ships Explorer/Monitors/Experiments/Observability. Single-vendor tools by design — a customer running Decagon for one workload and Sierra for another (common in larger enterprises) gets no cross-vendor scorecard from either.
- **Cloud LLM-eval SaaS** — leader: **[Braintrust](https://www.braintrust.dev/)**. Others: [LangSmith](https://www.langchain.com/langsmith), [Patronus AI](https://patronus.ai/). Strong text eval, but voice-specific primitives (WER on the buyer's entity dictionary, prosody / barge-in / interrupt-rate, audio-grounded hallucination) are not their product, and the regulated buyers we target won't ship audio to them anyway.
- **CCaaS-native QA modules** — **[NICE](https://www.nice.com/)**, [Genesys](https://www.genesys.com/) Quality Management, [Five9](https://www.five9.com/) WFO. Bundled with the call platform, large installed base, but model-agnostic regression eval against an arbitrary swap-in voice agent is not what they sell — and the enterprises adopting Decagon / Sierra / in-house agents are *replacing* the legacy CCaaS QA workflow, not extending it.

**Where the opening is.** The category that's missing is "private, audio-grounded, multi-vendor voice-agent regression eval that runs on the buyer's own recorded calls and reference dispositions." Hamming has the right product shape but the wrong deployment for regulated buyers. Cresta and Observe.AI have the audio and the dispositions but won't publish honest cross-vendor benchmarks because they sell the agents themselves. Decagon and Sierra ship single-vendor self-evals. Braintrust will not natively grow voice primitives. The CCaaS incumbents serve the legacy workflow. The wedge is a focused on-prem product whose first install is a 5-day sidecar that turns 90 days of the customer's own calls and CRM dispositions into a weekly cross-vendor scorecard the Head of Voice CX can hand their CFO when the model-swap question lands.

## Why us

- **Vincent led AI model evaluations at Amazon for 2 years — direct exposure to how a hyperscaler measures regression risk on non-deterministic AI systems at fleet scale.** That experience is generic AI eval, not code-specific; it transfers cleanly to a voice setting where the eval set is the buyer's own audio and the labels are the buyer's own CRM dispositions. The Amazon eval playbook is exactly what a 2,500+-agent voice-CX team is now scrambling to build internally.
- **Active depth in neuroscience, including auditory perception and prosody.** A voice-eval product that scores beyond transcript-equivalence — interrupt rate, backchannel selectivity, frustration detection — needs someone fluent in what the speech signal actually carries. Most LLM-ops founders don't have that vocabulary; the closest competitor (Hamming) was built by ex-Tesla data scientists and ex-Citizen infra, not speech / perception people.

## Customer & buyer

- **Customer:** **Head of Voice CX / VP of Conversational AI** at a 2,500+-agent contact center in BFSI (Gartner's named lead-adopter segment), healthcare payer/provider, telecom, or insurance, running ≥1 production voice agent at meaningful volume.
- **Buyer:** Same role, with **CTO / CIO / Chief AI Officer** sign-off above ~$200K. Budget line: contact-center technology + AI governance. Typical ACV: **$150K–$400K year-1**, growing with call volume and number of agents evaluated.
- **Champion:** **Director of Conversational AI / Voice Engineering** — the person responsible for the in-flight voice-agent rollout, who owns the Slack channel that lights up when CSAT drops on a Tuesday.
- **ICP test:** ≥2,500 contact-center agents + ≥1 production voice agent + a CCaaS-grade call recorder (Five9 / Genesys Cloud / NICE / Amazon Connect / Twilio) + a regulator or internal security policy that blocks shipping recorded calls to third-party SaaS (HIPAA, PCI, FINRA, EU GDPR, state-of-California consent).
- **Anti-customer:** Sub-100-agent SMB voice-agent shops (Hamming SaaS is fine for them); pure-cloud-native firms with no on-prem mandate; single-vendor shops with no second voice agent to benchmark against (cross-vendor scorecards are not the wedge for them — they should buy their vendor's native observability).

## Wedge / where we could enter

- **Candidate A — "Private τ-Voice for your call distribution."** A 5-day install that takes the customer's last 90 days of recorded calls + CRM dispositions, builds a stratified eval set, and produces a weekly per-vendor / per-prompt scorecard. Demo artifact-friendly, sharpest cold-pitch.
- **Candidate B — "Vendor-swap shadow-test."** Sit alongside the buyer's current voice agent (e.g., Decagon) and shadow-test a candidate alternative (open-weight, in-house, Sierra) on the same calls — answers the CFO's "save 70%?" question directly. Higher-stakes single decision, narrower category but easier to monetize as a project before the recurring scorecard kicks in.
- **Candidate C — "CCaaS-attached audio QA module."** Partner with Five9 / Genesys / NICE and sit inside their QA workflow as a model-agnostic eval module. Lower friction install, harder narrative ("yet another QA add-on"), and the partner could decide to build it themselves.

What pushes us to one: in the first 5 buyer conversations (with the artifact in front of them), do they gravitate toward "I need a number for my CFO" (→ A), "I need to decide on this specific model swap by Q3" (→ B), or "Make this invisible inside our existing QA team" (→ C). A is the default; B is the most likely six-figure design partner conversation; C is the channel play we'd take only if A and B both stall.

## What makes it defensible

- **(a) Primary — proprietary eval set per customer, made of their own audio + CRM dispositions.** Every customer's eval set is generated from their own recorded calls and grows weekly. After 6 months in production we know more about how each major voice agent vendor performs on *that customer's* call distribution than the customer or any vendor does. Switching cost is the eval set itself, the entity dictionary, and the disposition mapping — none of which is portable to a competitor.
- **(b) Secondary — multi-vendor benchmark across the customer base.** Anonymized cross-customer rankings ("Decagon vs. Sierra vs. in-house Pipecat on healthcare-payer claims-status calls, last 30 days") become a data product no single voice-agent vendor can publish credibly. This compounds with each additional customer in a vertical.
- **(c) Year-3 endgame — the private scorecard becomes the procurement standard.** Just as enterprises don't sign a database deal without TPC numbers, they stop signing voice-agent contracts without an Auralis scorecard. Becomes a soft tax on every Decagon / Sierra / Cresta / Observe.AI enterprise deal in the regulated-vertical segment.

## How it could make money

| Layer                                                                    | Price range          | Comparable                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------ | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Layer 1 — On-prem harness, per-call-volume**                           | $0.005–$0.02 / call evaluated  | [Cresta AWS Marketplace — $150K/yr per SKU, voice OR chat, at 100K voice calls / 125K chats](https://aws.amazon.com/marketplace/pp/prodview-lmdwown6xoo6q), [Hamming "1,000+ concurrent call stress testing" capability](https://hamming.ai/) |
| **Layer 2 — Multi-vendor regression scorecard + SLA alerts**             | $80K–$250K / yr      | [Patronus AI on AWS Marketplace, consumption-based](https://aws.amazon.com/marketplace/pp/prodview-qhhbedrtmc4zo), [Datadog LLM Observability](https://www.datadoghq.com/product/ai/llm-observability/) |
| **Layer 3 (later) — Cross-customer benchmark + vendor-bake-off reports** | $120K–$400K / yr     | [Cresta — Fortune 500 customer roster (annual contracts; pricing not published on homepage, see AWS Marketplace SKUs above for floor)](https://cresta.com/), [Observe.AI — 350+ enterprises (annual contracts; pricing not published)](https://www.observe.ai/) |

**Honest caveat.** The on-prem motion in regulated verticals is high-touch and slower than a cloud SaaS land — first 10 customers will look like services revenue dressed as license revenue. The remedy is to keep the harness install genuinely 5-day-able and refuse customizations that don't ship as product. Trap to avoid: turning into a bespoke voice-CX consultancy for one health insurer.

## What would pressure the thesis

1. **Assumption: regulated voice-CX teams will refuse to send recorded calls to third-party SaaS evaluators.**
   - **What would pressure it:** Hamming or a Cresta/Observe.AI competitor ships a credible single-tenant / customer-VPC deployment with the same UX as their hosted product, neutralizing the privacy wedge.
   - **Lever:** Re-anchor the wedge from "privacy" to "your own dispositions are the only ground truth that matters" — a private-VPC hosted product still needs the customer to manually build the eval set, and the disposition-grounded labeling pipeline is harder to replicate than the deployment shape.
2. **Assumption: voice-CX teams will pay for cross-vendor regression-eval separately from CCaaS QA and from the voice-agent vendor's native observability.**
   - **What would pressure it:** Cresta or Observe.AI ships a credible multi-vendor benchmark module bundled into their existing license, OR Decagon / Sierra publish their own honest cross-vendor scorecards (unlikely but not impossible if a third-party benchmark like τ-Voice forces the issue).
   - **Lever:** Lean on "the rep dispositions are *your* data, not theirs" — neither the agent vendor nor the QA incumbent can match a buyer-private eval set tied to the buyer's own CRM ground truth.
3. **Assumption: the voice-agent market remains multi-vendor enough for cross-vendor scoring to matter.**
   - **What would pressure it:** Market consolidates to a single dominant voice-agent vendor (e.g., Sierra absorbs the SMB segment and the enterprise default).
   - **Lever:** Pivot from cross-vendor to cross-prompt / cross-model regression on the dominant vendor — "did the Tuesday prompt edit hurt CSAT" survives consolidation.
4. **Assumption: the 47-point voice-vs-text capability gap (τ-Voice) persists long enough for an eval-heavy buyer behavior to become routine.**
   - **What would pressure it:** Native-audio frontier models close the gap fast and voice agents start hitting 80%+ on realistic conditions, which makes regression-eval a once-a-quarter activity rather than a weekly one.
   - **Lever:** Convergence still leaves the buyer asking "did *my* swap regress *my* call distribution" — the absolute scores converge, the deltas don't.

## 2-week experiment

**Load-bearing assumption to test:** A Head of Voice CX at a 2,500+-agent regulated firm, after seeing a working private scorecard built from a public-but-realistic call corpus, will give 30 minutes, name a budget line, and identify a person who could buy.

**Artifact to build (week 1):** A working v0 of Auralis running against a public call corpus that's a proxy for an enterprise contact center — pick a public dataset like the [PolyAI MINDS-14](https://huggingface.co/datasets/PolyAI/minds14) banking corpus or [Switchboard](https://catalog.ldc.upenn.edu/LDC97S62) — and:

1. Build an eval set of 200 calls with synthesized "CRM dispositions" (intent + outcome) extracted from the transcripts as ground-truth labels.
2. Replay each caller-side audio against three voice-agent configs running locally on the demo laptop: an OpenAI Realtime API agent, a Pipecat + Deepgram + GPT-4o-mini stack, and an open-weight Kimi K2.6-voice + ElevenLabs stack.
3. Score each config on five layers: WER on a hand-curated banking entity dictionary, intent/disposition match rate vs. ground truth, hallucination rate (AssemblyAI 5+-consecutive-error definition, validated by tool-call diff), p95 turn latency, and policy-gate adherence on a 10-rule script.
4. Publish the result as a *private demo URL* (not a public leaderboard — that forces vendor PR conversations we don't want yet) showing per-config scorecards, week-on-week deltas, and a "regression alert" view.
5. Record a 7-minute screencast walking through one regression discovered live (e.g., "Pipecat + Deepgram dropped 11pp on intent-match after Deepgram Nova-3 → Nova-3.1 upgrade").

The artifact must run locally with no outbound calls during demo (proves the privacy story).

**Conversations (week 2):** 8–10 named Head-of-Voice-CX / Director-of-Conversational-AI leads at 2,500+-agent firms, sourced via Vincent's INSEAD network (financial services, telco), Amazon contacts (e.g., Connect customers in healthcare and BFSI), and 2–3 warm intros into European banks and Japanese insurers. Each call opens with the screencast, then the live demo on Vincent's laptop using a sample of the buyer's own publicly-released call snippets if available, otherwise the public-corpus demo.

**Specific questions / asks:**
1. "If this scorecard ran inside your VPC, on your last 90 days of calls, would you install it next quarter? If no, what's missing?"
2. "Who owns the budget — you, the CTO, the CIO, AI governance, the VP of Customer Service?"
3. "Which voice agents are you running today, and how do you currently know if a model upgrade made things worse on your callers?"
4. "What would you need to see to sign a $200K design-partner contract for the next 12 months?"
5. "What's the one regression you wish you'd caught last quarter — and how did you eventually catch it?"

**Pass criteria:** ≥3 design-partner LOIs (or written commitment to a paid pilot) AND ≥1 buyer names a PO date within the next quarter AND the screencast gets ≥150 thoughtful inbound signals (replies, "send me access" emails, HN comments) when posted to the LLM-ops / contact-center corner of the internet at the end of week 2.

**Kill criteria:** ≤1 LOI, no named PO date from any conversation, AND <40 inbound signals on the screencast → walk away. The privacy/quality gap was either not real or not painful enough to pay for.

**Vincent's effort:** ~75 hours total. ~50 on the artifact (build + screencast), ~25 on outreach + 8–10 calls + memo. Output: live demo URL, screencast, memo with quoted answers from each call, and a go / pivot / kill recommendation.

## What we don't know yet

- Whether the on-prem deployment shape can be made to feel like SaaS install-time (5 days) or whether regulated buyers force a 6-week professional-services motion that breaks the unit economics.
- How fast Hamming or a Cresta/Observe.AI competitor will ship a credible single-tenant deployment, and whether they'd partner or compete.
- Whether the disposition-as-ground-truth labeling pipeline holds up across verticals (BFSI vs. healthcare payer vs. telecom) without per-vertical custom work.
- Whether a Tokyo / Paris go-to-market really pulls ahead of a SF default given the current voice-agent vendor concentration in the US.

## Vincent's Feedback

**Disposition: pass.** The buyer pain is real and the founder-fit is direct (Amazon evals + auditory perception), but the eval methodology as drafted doesn't survive scrutiny, and the value-chain layers that *do* work don't align with a Vincent-shaped moat.

**Fatal flaw in the methodology.** The proto says "replays each call's caller-side audio against the candidate agent" as if calls were static inputs. They aren't — a real call is `caller_t1 → rep_t1 → caller_t2 (responding to rep_t1) → ...`. If the candidate agent's `t1` differs from the rep's, every subsequent caller turn is a non-sequitur, and the dialogue becomes gibberish by turn 3-4. The "your own recorded calls are your eval set" hook only works for single-turn / IVR-replacement evals — useless for the multi-turn collections / claims / scheduling workflows the proto names as the buyer.

The rescue is to build a caller-simulator from the historical data and run candidate agents against it (which is what Hamming actually does), but that eats the on-prem-audio moat: you're now selling a synthetic-cohort eval seeded from CRM exports, not a unique-because-it-uses-your-real-audio eval. CRM dispositions without raw audio are exfiltrate-able by any Hamming-class competitor.

**Value chain decomposed (worth keeping for future bets).**

1. **Horizontal — caller-simulator from historical data.** Turn `(caller audio, intent, outcome, context)` into a persona-grounded LLM caller-sim. Most contested layer. Hamming, Coval, plus the agent vendors themselves (Decagon Optimize, Sierra Experiments) all working it.
2. **Horizontal — scoring primitives.** WER, intent-match, hallucination definitions, latency percentiles, outcome-match against historical dispositions, policy-gate adherence. Same primitives across verticals once the simulator exists. Hamming, Patronus, Braintrust+voice-extensions all working this layer.
3. **Vertical — entity dictionaries, domain failure modes, regulatory/compliance rubrics, CCaaS/CRM integrations.** Banking entity vocab ≠ healthcare payer vocab; HIPAA-PHI scoring ≠ FINRA call-recording rules; Five9 vs Epic vs Salesforce hooks differ. Real work, not durably defensible — incumbents can build it once they care, and verticalization typically dilutes margin rather than concentrating it.
4. **Deployment / security architecture.** On-prem / customer-VPC, single-tenant, audited data flows. The original proto's wedge. Execution-thin — Hamming or Cresta ships single-tenant in a quarter once a regulated buyer asks twice.

**Where Vincent's founder-fit actually points.** Every layer above is contested or commoditizing, and none aligns with a structural advantage. Generic eval methodology + Amazon-evals experience helps build the product but doesn't moat it. The one place the founder-fit *does* point at a structural moat is **audio-acoustic / prosody scoring** — interrupt rate, backchannel selectivity, prosody match, frustration detection — where eval-tooling shops are weakest because it's not text-LLM-judgeable, and where neuroscience + auditory perception is genuinely rare in the founder pool. That's the same adjacent space flagged in Mensho's feedback (TTS-prosody quality eval for non-English locales). Loop closing — that's a possible bet, separate from this regression-eval-harness framing.

## Related

- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]]
- [[Touchstone — Per-variant evals so the bespoke-software era doesn't ship a million silently-wrong internal tools]]
- [[Stentor — Agent-native commerce surface for medical-imaging and lab-diagnostics vendors selling into hospitals where AI agents now sit on the buyer side]]
