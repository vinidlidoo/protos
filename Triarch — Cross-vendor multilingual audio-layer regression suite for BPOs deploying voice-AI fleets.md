---
id: proto-triarch
aliases:
  - Triarch
tags:
  - proto
type: proto
status: drafted
created: 2026-05-04
origin: ""
proto_generator:
  seed: 908414520
  writer: 1
  writers_total: 1
  repo_sha: 04e128d
  generated_at: 2026-05-04T19:38:16+00:00
---

# Triarch — Cross-vendor multilingual audio-layer regression suite for BPOs deploying voice-AI fleets

## What is it?

**Elevator pitch**: Triarch sells a mid-tier BPO's VP of CX Operations a vendor-neutral, audio-layer scorecard that ranks the voice-AI vendors they're deploying — Decagon vs. Regal vs. Vapi — on the BPO's own client calls in Japanese, French, and English. What changes Friday: the program lead can finally answer "which vendor should ship into our JP queue this week" with a number their floor supervisors trust, instead of a six-week manual A/B. The CCaaS QA incumbents (Five9, NICE, Genesys) cannot build this — they're locked to their own audio bus and would have to evaluate vendors competing with their parent's roadmap.

**How it works**: The BPO uploads ~5,000 of the client's last-90-days human-agent calls (recorded under existing data-processor agreements). Triarch fingerprints the calls per language and call type — typical interrupt cadences, opening-greeting prosody envelopes, register-shift triggers (keigo, tutoiement). Each candidate voice-AI vendor's API is then driven through a **first-three-turn replay harness**: the customer's recorded opening, the agent's response, the customer's first follow-up, the agent's second response. The harness scores audio-layer behavior on those bounded surfaces — opening greeting prosody, disclosure-register adherence, interrupt-handling on the customer's first interruption — where the recorded customer turns are still in-distribution. A Large Audio Language Model judges prosody and register; narrow specialist heads handle interrupt-detection and latency. We deliberately do not extend the replay past turn 3; everything past that point is a different methodology (live shadowing, see Layer 2 in pricing) and the proto explicitly does not claim replay-eval for full multi-turn dialogues.

## What's the problem?

The BPO program lead is on the hook for 50%-cost-reduction outcomes their client signed for, but they don't pick the voice-AI vendor — the client did, sometimes two of them. Today the BPO has no way to ship the *right* AI vendor into the *right* language queue at the *right* moment. Their two existing tools — the CCaaS QA suite (Five9 AQM, NICE CXone, Genesys) and the vendor's own metrics — are both text-LLM-based scorecards, and both miss audio-layer failures (TTS prosody collapse, interrupt mishandling, register breaks in JP/FR) that are exactly what blow up CSAT in non-English markets. The program lead either runs a multi-week manual A/B with their floor supervisors (slow, judgment-soaked, doesn't scale across 10+ languages) or ships blind and hopes the CSAT trend is acceptable. Both options burn the margin the BPO promised.

## Why now (2026)

- **BPO-side voice-AI rollouts are now a 2026 contractual reality, not a 2027 forecast.** TaskUs partnered with Decagon and Regal in 2025; Concentrix's iX Hello and iX Hero AI platforms were [in nearly 40% of new client wins in 2025](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/); TP launched its [TP.ai FAB orchestration platform](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/) under a €100M AI partnership program; Alorica's evoAI [manages nearly half of enterprise interaction volume in deployments](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/). Multi-vendor voice-AI inside a single BPO program is the operating reality, not the future state.
- **The CCaaS QA layer scores transcripts, not audio.** Five9's [Agentic Quality Management evaluates up to 100% of customer interactions](https://www.five9.com/news/news-releases/five9-launches-new-genius-ai-innovations-accelerate-agentic-cx-five9-cx-summit) and NICE's [Quality Management uses generative AI to Auto Score for 100% unbiased evaluation coverage across voice and digital channels](https://uk.nice.com/products/quality-management); both rely on transcript-grounded LLM judging. None of their public capabilities describe audio-layer scoring (prosody envelope, interrupt rate, backchannel selectivity) — the layer where multilingual voice-AI most visibly fails.
- **Published 2025–26 audio-LLM benchmarks confirm the audio-layer gap is real, not hypothetical.** The DEAF benchmark of 2,700 conflict stimuli found that under combined semantic-and-prompt pressure, [emotional-prosody robustness collapses below 7% for nearly every Audio MLLM tested](https://arxiv.org/html/2603.18048v2) — they default to text-driven inference. SpeechRole-Eval found that even GPT-4o Audio is [limited in prosody consistency and emotion appropriateness](https://arxiv.org/html/2508.02013v7). EmergentTTS-Eval shows fine-grained prosodic failures across 11Labs, Deepgram, and OpenAI 4o-mini-TTS that [conventional metrics overlook](https://arxiv.org/html/2505.23009v1).
- **The global call-center outsourcing market is $121B → $199B by 2032 with $80B of agent labor cost reduction Gartner-projected for 2026 alone.** Source: [Gartner cited in 2026 BPO landscape report](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/) — at this rollout pace, every margin point a BPO loses to a wrong-vendor-in-wrong-language deployment is real money, and they don't have a tool to prevent it.
- **Multilingual is structurally where this hurts.** [Foundever handles 9M+ daily customer conversations across 60+ languages](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/); [Alorica's ReVoLT covers 75 languages and 200 dialects](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/); [TELUS Digital's Fuel iX annotates in 500+ languages](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/). The audio-layer failure modes that DEAF/MSPB document are exactly what the multilingual rollout surface stresses; English-only QA was good enough for the English-dominant decade.

## Who else is doing this

- **CCaaS-bundled QA platforms** — main player: **[NICE CXone Quality Management](https://uk.nice.com/products/quality-management)** (gen-AI auto-scoring of voice + digital). Others: [Five9 AQM](https://www.five9.com/news/news-releases/five9-launches-new-genius-ai-innovations-accelerate-agentic-cx-five9-cx-summit), [RingCentral AVA Supervisor Assist](https://ringcentral.com/ringcx/ai-supervisor-assist.html). All transcript-grounded LLM scoring; all locked to their own audio bus; none cross-vendor; none audio-layer.
- **Real-time agent-assist + auto-QA point tools** — main player: **[Balto](https://www.balto.ai/real-time-qa)** (real-time supervisor alerts, 100% call scoring, agent-app feedback). Others: [Invoca](https://www.invoca.com/product/quality-management) (voice analytics QA), [ConvoZen](https://convozen.ai/product/supervisor-ai-agent) (omnichannel supervisor agent), [Zowie Supervisor](https://getzowie.com/supervisor) (AI-and-human interaction scoring), [Tactful Supervisor Hub](https://tactful.ai/platform/supervisor). These are human-agent-supervisor tools sold to enterprise buyers, not BPOs evaluating multiple AI vendors.
- **In-house BPO orchestration platforms** — main player: **[TP.ai FAB](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/)** (Foundational AI Backbone). Others: [Concentrix iX Hello / iX Hero](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/), [Alorica IQ + evoAI](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/), [TaskUs Agentic AI](https://www.taskus.com/services/agentic-ai/). These are the BPOs' own platforms; they're built to integrate AI *into* the BPO's delivery, not to evaluate third-party AI vendors comparatively. The smaller BPOs (~$1B revenue and below) cannot afford to build them and are exactly the ICP.
- **Academic & vendor-side audio benchmarks** — main player: **[EmergentTTS-Eval](https://arxiv.org/html/2505.23009v1)**. Others: [DEAF](https://arxiv.org/html/2603.18048v2), [SpeechRole-Eval](https://arxiv.org/html/2508.02013v7), [MSPB](https://www.isca-archive.org/interspeech_2025/wang25v_interspeech.pdf). Research-grade and vendor-side; none are productized for buyer-side comparative procurement.

**Where the opening is**: BPOs don't have a vendor-neutral, audio-layer, multilingual workbench because no incumbent is positioned to build one. CCaaS QA platforms are locked to their own audio bus and cannot evaluate vendors competing with their parent's ecosystem. The mega-BPOs' in-house platforms (TP.ai FAB, iX Hero) are built to make their own delivery look good, not to compare third-party vendors objectively. The academic benchmarks score TTS systems, not deployed-in-context voice agents. The seam — the BPO program lead who must comparatively grade two voice-AI vendors on the same client's JP/FR/EN call types this Friday — is owned by no one.

## Why us

- **Trilingual EN/FR/JA + Amazon AI-evaluations background = unusually rare combined founder-fit for the audio-layer multilingual rubric.** Native-level fluency in three of the [60+ languages Foundever serves daily](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/) and direct exposure to how a hyperscaler measures AI quality, regression, and risk — the exact two skills required to author the rubric that anchors the moat.
- **Auditory-perception + neuroscience depth maps to the prosody / interrupt-rate / register-shift scoring layer that text-LLM judges miss.** This is the layer DEAF and MSPB benchmarks identify as where current models fail; the rubric is not LLM-judgeable text and won't be commodified by a frontier-model upgrade.

## Customer & buyer

- **Customer:** Mid-tier BPO program lead (Director-level) running a single client's multi-vendor voice-AI deployment across ≥3 languages.
- **Buyer:** VP of CX Operations or Director of AI Programs at a mid-tier BPO ($200M–$1B revenue band, where a Chief AI Officer role typically does not exist yet). Budget line: AI tooling within the BPO's CX-delivery P&L (not the client's). Typical ACV: $80K–$200K Year-1 for the first program; expands to $300K+ as the BPO rolls Triarch into additional client programs.
- **Champion:** the program's CX-Quality director — the role currently maintaining manual evaluation calibration scorecards and absorbing CSAT regressions when a vendor swap goes wrong.
- **ICP test:** mid-tier BPOs ($200M–$1B revenue) with ≥2 active voice-AI vendor deployments, ≥3 supported languages, public commitments to cost-reduction targets in client contracts, and at least one CSAT regression incident in the last 12 months that triggered a vendor-swap conversation.
- **Anti-customer:** the mega-BPOs that have already built (TP, Concentrix, Alorica, TaskUs) — they will buy on tactical short-term gaps but their long-term play is to absorb. Sell to them after we win 5 mid-tier reference accounts, not before; until then they're 1 of 8 validation-only conversations, not the wedge.

## Wedge / where we could enter

- **Candidate A — Single-language Japanese pilot with one mid-tier BPO operating in JP.** The audio-layer + multilingual gap hurts most where the language is far from English and the prosody/register surface is rich. Vincent's JP fluency makes this the highest-conviction landable beachhead.
- **Candidate B — JP+FR pilot with a European-anchored BPO.** Transcom (Sweden, [33 languages, 90+ contact centers](https://aitoptools.com/ai-blog/top-10-call-center-outsourcing-companies-using-ai-to-transform-customer-support/)) or Foundever (Luxembourg) could anchor a Europe-first launch. Slower-cycle but bigger ACVs once landed.
- **Candidate C — Open-source benchmark first, BPO sale later.** Publish a public Triarch-Bench scorecard ranking Decagon, Regal, Bland, Vapi, Cartesia, Sesame on JP/FR audio-layer dimensions; let inbound BPO interest pull the commercial wedge. Highest awareness build, slowest revenue path.

What would push us toward A: a single mid-tier BPO program lead in Tokyo with a multi-vendor JP rollout already underway saying the words "we have no good way to grade these comparatively." That conversation is achievable in the 2-week experiment.

## What makes it defensible

- **(a) Primary: per-BPO, per-client audio fingerprints — the calibration layer, not the rubric.** The recurring-revenue product is the ongoing recalibration of each buyer's fingerprint as their client's call mix, vendor mix, and language mix shifts month over month. The rubric ("score prosody envelope similarity to baseline") may be reproducible by a frontier audio model; the fingerprint ("this BPO's specific keigo-vs-casual register distribution across these 14 client queues, recalibrated weekly") is not, because the audio data and the recalibration cadence are buyer-specific. This is a deliberate choice: we treat the rubric as commodity and the calibration as the product, so frontier-model parity on prosody scoring is a tailwind (cheaper judge), not a kill.
- **(b) Secondary: cross-vendor leverage that the CCaaS incumbents structurally cannot match.** Once 3+ BPOs use Triarch, the comparative scorecards across Decagon, Regal, Bland, Vapi become a procurement-grade benchmark voice-AI vendors want to be measured by. CCaaS incumbents (Five9, NICE, Genesys) can't credibly publish this — they would have to evaluate vendors that compete with their own roadmap, and their audio bus is locked to their own platform.
- **(c) Year-3 endgame:** become the de facto pre-procurement audio-layer benchmark voice-AI vendors self-publish against, the way SOC-2 happened to security or MMLU happened to LLM reasoning. The Triarch-Bench public scorecard is the distribution channel; the BPO calibration subscription is the revenue.

## How it could make money

| Layer               | Price range | Comparable        |
| ------------------- | ----------- | ----------------- |
| **Layer 1: BPO subscription — first-three-turn replay scorecard, per program** | $80K–$200K ARR per BPO program | [NICE CXone QM enterprise contracts](https://uk.nice.com/products/quality-management) bracket the BPO-tier QM-tooling line item |
| **Layer 2: live shadowing add-on (multi-turn audio scoring on live calls, sidesteps replay-divergence)** | $150K–$400K ARR per program | [Balto's real-time QA per-license tooling](https://www.balto.ai/real-time-qa) |
| **Layer 3 (later): public Triarch-Bench scorecard with paid private deltas for vendors** | $100K–$500K / voice-AI vendor for private detailed delta vs. their published score | [Aceyus VUE / OneVUE multi-vendor analytics tier inside Five9](https://www.five9.com/news/news-releases/five9-launches-new-genius-ai-innovations-accelerate-agentic-cx-five9-cx-summit) |

**Caveat:** Layer-1 demands the BPO accept that we score vendors *they* picked unfavorably, which is a politically loaded conversation. We need at least one BPO champion who's already been burned by a vendor swap to land the first deal — without that scar, the buyer doesn't pre-emptively buy a tool that may produce uncomfortable findings.

## What would pressure the thesis

1. **Assumption:** BPOs (not voice-AI vendors, not enterprise voice-customers) are the right buyer because they own the contracted-outcome consequence and have multi-vendor deployments.
   - **What would pressure it:** in 2-week-experiment interviews, BPO program leads say their clients pick the vendor and own the QA, with the BPO operating the deployment but not graded on AI-quality outcomes. If the contractual structure shows the BPO is shielded from AI-quality risk, the wedge is wrong.
   - **Lever:** pivot buyer to the BPO's *client* (the brand running the multi-vendor stack) as a procurement-side tool used during AI-vendor selection.
2. **Assumption:** Audio-layer rubrics (prosody, interrupt rate, code-switch) are buyer-judgeable as actually predictive of CSAT, not just academically interesting.
   - **What would pressure it:** the artifact's first scorecard ranks vendor X above vendor Y but the BPO's own CSAT data ranks them the other way. If the rubric doesn't correlate with downstream CSAT, the moat collapses.
   - **Lever:** publish the correlation table early; if the audio-layer rubric is weakly predictive of CSAT, lean harder on the *interrupt-handling and disclosure-compliance* sub-rubrics, which translate directly to call-completion and regulatory exposure.
3. **Assumption:** The replay harness's first-three-turn scope is genuinely useful to BPO buyers — they care enough about opening-greeting prosody, first-disclosure register, and first-interrupt handling to subscribe, even though full-dialogue scoring is out of scope until Layer 2.
   - **What would pressure it:** in week-2 interviews, ≥4 of 8 BPO program leads say they need full-call scoring to make a vendor-swap decision and that opening-turn-only data is not actionable. If turn-3-cap data fails the actionability test, the wedge collapses to live-shadowing-only (Layer 2), which is a slower, more expensive product to ship.
   - **Lever:** if turn-3-cap fails, lead with Layer 2 (live shadowing on a small percentage of in-flight calls) as the wedge, accept the longer build cycle, and use the public Triarch-Bench scorecard (turn-3-only) as the awareness channel rather than the revenue product.

## 2-week experiment

**Load-bearing assumption to test:** that a BPO program lead running a multi-vendor JP voice-AI deployment will, in 30 minutes with the artifact in front of them, both (a) confirm the comparative-scoring problem is unowned today, and (b) name the audio-layer dimensions they'd grade vendors on.

**Artifact to build (week 1):** A public **Triarch-Bench JP-pilot scorecard**: scrape ~50 publicly available Japanese customer-service conversations (corpus already exists on HuggingFace / Common Voice JP / consenting podcasts), run them through 3 voice-AI vendor APIs (Decagon, Regal/equivalent, Vapi or one Japanese vendor like Allganize), score the audio outputs on 6 dimensions (prosody envelope similarity, interrupt rate, backchannel cadence, keigo register adherence, code-switch handling EN↔JP, latency p95), publish the scorecard with audio clips at triarch-bench.dev. Architecture: a single FastAPI service + an LALM judge (GPT-4o Audio or Gemini 2.5 Pro Audio) for prosody scoring + 1 narrow specialist head for interrupt detection. Build target: 5 working days solo with coding agents.

**Conversations (week 2):** 8 conversations, weighted to the mid-tier ICP. **One** mega-BPO interview as a validation check (TaskUs JP — they're in the Decagon/Regal multi-vendor world and the contrast against mid-tier reactions is informative). **Seven** mid-tier BPOs operating in JP and FR — Bell24, Pasona JOB HUB, Tokyo Customer Service (TCS-J), TMJ, transcosmos, Almex (JP-anchored), and one French/Quebec mid-tier (Webhelp pre-Concentrix-merger alumni network or Acticall-spinout). Each conversation opens with the live scorecard pulled up on screen — they look at it, react, push back on the rubric, name dimensions we missed, point at the vendor they'd grade lower / higher than we did and tell us why.

**Specific questions / asks:**
1. Looking at this scorecard, which dimension would you most want to add or remove for your current rollout?
2. If you saw vendor X scoring 30% lower than vendor Y on register adherence, what would change in your operating decisions next week?
3. Who in your org owns this comparative-grading question today? Is that role budgeted? What does it cost the program when they get it wrong?
4. Would you give us 100 of your client's recorded JP calls (under your existing data-processor agreement) to fingerprint your specific deployment for a 30-day pilot?

**Pass criteria:** ≥5 of 8 BPO interviews confirm the role-and-pain hypothesis; ≥2 commit to a paid 30-day pilot with their client's audio data; the public Triarch-Bench scorecard gets ≥1 voice-AI vendor reaching out to dispute / request a methodology session (the asymmetry signal); at least one BPO buyer pulls out a Q3 2026 PO timeline.

**Kill criteria:** ≤2 of 8 interviews confirm the pain (program leads say their clients own QA and they don't get to comparatively grade); the scorecard's audio-layer scores correlate <0.4 with the BPOs' own CSAT data; or no voice-AI vendor responds within 14 days of public posting (signals the comparative-benchmark moat doesn't matter to them yet).

**Vincent's effort:** ~80h: 50h build (5 working days), 30h conversations (8 × ~3h prep+meet+memo). Output: triarch-bench.dev live scorecard + a memo with quoted answers + a go / pivot / kill recommendation.

## What we don't know yet

- Whether the BPO can legally share recorded customer calls with us as a third-party data processor without re-consenting customers (the data-processor flow under JP APPI / EU GDPR matters here).
- Whether Decagon, Regal, Bland, Vapi, etc. expose the API surfaces required for a faithful replay of the BPO's recorded conversations (some may only allow live inference, not corpus-replay scoring).
- Whether mid-tier BPOs can buy at $200K+ ACV — the spread between mega-BPO and mid-tier BPO budget is wide and we should pressure-test the lower bound.
- Whether the JP-FR-EN trilingual rubric scope is the right starting language set or whether a BPO would prefer JP-only depth before geographic expansion.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Auralis — Private regression-eval harness for enterprise voice-agent fleets where the buyer's own recorded calls are the eval set]]
- [[Mensho — Multilingual cultural-rubric eval suite voice-AI vendors plug into CI to ship Japanese, French, and code-switching deployments without quality regressions]]
- [[Banto — Voice-first generative interface that turns a Japanese ryokan's own service standards into a per-shift operating system for the floor]]
