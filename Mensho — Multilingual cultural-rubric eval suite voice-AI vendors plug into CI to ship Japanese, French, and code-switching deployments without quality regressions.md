---
proto_generator:
  seed: 7734679
  writer: 1
  writers_total: 3
  repo_sha: aba8ddf
  generated_at: 2026-05-01T06:03:27+00:00
id: proto-mensho
aliases:
  - Mensho
tags:
  - proto
type: proto
status: passed
created: 2026-05-01
origin: ""
---
# Mensho — Multilingual cultural-rubric eval suite voice-AI vendors plug into CI to ship Japanese, French, and code-switching deployments without quality regressions

## What is it?

**Elevator pitch.** Mensho is the eval suite a voice-AI agent vendor (Retell, Synthflow, Vapi, Bland, PolyAI, Replicant) plugs into its CI to prove its agent doesn't regress on **Japanese keigo, French formality, Spanish/English code-switching, and other locale-specific cultural rubrics** when it swaps a model, voice, or prompt. The vendor's AI-engineering lead pays so that the next time their RFP team is asked "how do you guarantee this won't insult my Japanese customers," they have a graded scorecard with examples, not a hand-wave.

**How it works.** A vendor pipes a sample of their production calls (or a synthetic test set we co-author) through Mensho per CI run. Each call is scored along language-specific rubric dimensions — for Japanese: keigo register accuracy, *teineigo*/*sonkeigo*/*kenjōgo* mix, *aizuchi* timing; for French: tu/vous switching, register break detection, regional politeness norms; for code-switching: language-switch latency, untranslated-term policy adherence. Rubrics are designed by native-speaker linguists Mensho contracts; scoring runs as LLM-as-judge with native-speaker calibration sets. Every model swap, prompt edit, and voice change produces a delta dashboard the vendor's AI-eng lead can ship to their customer's procurement team. Failed evals block the deploy.

## What's the problem?

Voice-AI vendors building on top of OpenAI Realtime, Gemini Live, and the open STT/TTS stack are now winning enterprise deals — but their quality story stops at the English customer base. When a Japanese bank, a French insurer, or a Mexican-American bilingual healthcare payor runs a procurement, the vendor's eval suite scores intent accuracy and turn latency, not "does this voice say *moushiwake gozaimasen* at the right register" or "did the agent switch to *vous* when the caller signaled they were a senior." The vendors patch case-by-case after launch, get burned by a viral failure (an AI sales call that "felt creepy" went around JP X in April 2026), and lose the next regional deal. There is no productized regression-test layer for cultural-linguistic quality.

## Why now (2026)

- **The voice-AI agent stack is on a 34.8% CAGR trajectory from $2.4B in 2024 to a projected $47.5B by 2034** ([Market.us Voice AI Agents Market report](https://market.us/report/voice-ai-agents-market/)). And vendors like Retell already meter "AI Quality Assurance" as a $0.10/min add-on with first 100 minutes free ([Retell AI pricing](https://www.retellai.com/pricing)) — eval-as-line-item is established price discovery, not a category invention.
- **Per-minute voice-agent platforms ship in days, not quarters.** Retell publishes pay-as-you-go pricing at $0.07–$0.31/min with 20 free concurrent calls, $10 starting credits, and "go live in minutes, no commitments" ([Retell AI pricing](https://www.retellai.com/pricing)). When deployment is fast and cheap, the surviving moat is **trust on output quality** — and that's where the regression-test layer lives.
- **Even the multilingual leader admits dialect and code-switching are out-of-the-box gaps.** PolyAI lists 12 supported languages by default, but explicitly notes "regional variants, dialect-specific tuning, and code-switching are only available through custom enterprise agreements" ([PolyAI multilingual review via Synthflow](https://synthflow.ai/blog/polyai-review)). The headline category leader treats cultural-linguistic depth as bespoke services revenue — meaning the *long tail* of vendors below them have nothing.
- **The Japanese-ASR-on-LLM research baseline is fresh and shallow.** The first GER (generative-error-correction) benchmark for Japanese ASR was published in late 2024 with 0.9–2.6k text utterances ([Ko et al., arXiv 2408.16180](https://arxiv.org/abs/2408.16180)) — a research-grade dataset, not a productizable eval suite for keigo register, regional dialect, or live conversation. The gap between research benchmarks and shippable vendor-side regression tests is exactly what a productized eval is for.
- **Japan's AI Promotion Act is innovation-first, not penalty-driven.** The Act passed in May 2025 with no monetary penalties and only "name-and-shame" enforcement; vendors are not buying because of a compliance clock ([White & Case on Japan AI Act](https://www.whitecase.com/insight-alert/japans-first-ai-legislation-becomes-law-focus-promoting-research-and-development-no)). They are buying because **a single bad call in a localized market kills the regional contract**. Demand is reputational, not regulatory — exactly the right shape.
- **Live X discourse is now flagging multilingual voice-quality "collapses."** A detailed April 30 evaluation of a JP voice deployment described intonation that sounded like a Chinese accent and speaker-assignment errors as a "collapse" ([@user JP voice eval, 2026-04-30](https://x.com/i/status/2049733553207083342)); a viral Japanese complaint of an AI sales call with "creepy processing pauses" surfaced April 17 ([@user JP AI call complaint, 2026-04-17](https://x.com/i/status/2045037796490940573)). Vendors see these as one-off social incidents; in aggregate they're the regression signal a CI gate would have caught.

## Who else is doing this

- **Contact-center incumbents with built-in quality scoring** — main player: **[Cresta](https://cresta.com/ai-platform)** ("Cresta combines rigorous LLM-based evaluation, evidence-based reasoning, simulation testing, and regression testing"). Others: **[Observe.AI](https://www.observe.ai/)** ("Automatically QA 100% of human and AI interactions"), **[Level AI](https://thelevel.ai/)**. These score *the BPO's deployment*, not the vendor's pre-ship CI; their rubric depth is English-first, and they sell to the BPO buyer rather than the AI-vendor product team. They don't slot into a Vapi/Retell vendor's CI pipeline before deploy.
- **Generic LLM-eval and observability platforms** — main player: **[Braintrust](https://www.braintrust.dev/pricing)** ($249/mo Pro, $1.50/1k scores). Others: [LangSmith](https://www.langchain.com/langsmith), [Langfuse](https://langfuse.com/), [Patronus AI](https://patronus.ai/). Powerful eval primitives; the buyer writes the rubric. Nobody ships keigo or French-formality rubrics; nobody contracts native-speaker calibration. The eval engine is generic; the cultural-rubric corpus is not.
- **Japanese-domestic voice-analytics incumbents** — main player: **[MiiTel by RevComm](https://www.revcomm.com/en/news/pressrelease/voice-analysis-ai-miitel-exceeds-110000-total-users-and-3000-companies/)** ("Voice analysis AI 'MiiTel' exceeds 110,000 total users and 3,000 companies"). Voice-analytics for *human* sales-agent coaching, not regression-testing for AI agents. Domestic distribution moat in JP, but no CI-pipeline product, no English-vendor partnership story, and no French/Spanish coverage.
- **Voice-AI vendors' own internal eval** — every Retell, Vapi, Synthflow, Bland, PolyAI ships some eval scaffolding (Retell mentions "Simulation Testing" in its base plan). Internal eval bench engineering attention is finite; they will keep building English-first quality and outsource the localization-rubric depth — same way Stripe outsourced anti-fraud-as-a-service to Sift instead of staffing a fraud team in-house.

**Where the opening is.** The buyer is the **voice-AI vendor's AI-engineering lead** trying to ship a procurement-defensible quality story for non-English markets. The contact-center QA incumbents sell post-deploy to the BPO. The eval-platform horizontals sell rubric primitives but leave native-speaker calibration to the customer. The Japanese voice-analytics incumbents sell coaching for human agents. None of them gives a Retell or PolyAI a one-line CI step that says "your new GPT-5.4 swap regressed keigo accuracy 8% on the Tokyo bank corpus — block deploy." That CI step is what Mensho sells.

## Why us

- **Trilingual EN/FR/JA cultural-fluency at native-speaker depth across three of the world's largest economies is the moat.** Most US-based eval shops cannot even *grade* a keigo register error or a French tutoiement violation themselves; they would have to hire and manage a linguist supply chain Vincent has lived inside for decades. Building the rubric corpus is the year-one work, and Vincent's network is the year-one supply.
- **Direct experience leading AI model evaluations at Amazon supplies the customer-side mental model.** Vincent knows what an AI-eng lead actually wants to see (regression deltas, calibration sets, false-positive budgets, a corpus that survives a model swap), what they discard (vibes-based "quality scores"), and what kills the pilot (a rubric the AI-eng lead can't reproduce internally).

## Customer & buyer

- **Customer:** AI Engineering Lead or Quality Lead at a voice-AI agent platform vendor (Retell, Vapi, Synthflow, Bland, PolyAI, Replicant) or a vertical voice-AI app vendor (a healthcare voice-scribe, a hospitality concierge, an outbound-sales SDR product) targeting non-English markets.
- **Buyer:** VP Engineering or VP Product at the vendor; budget pulls from "AI Quality / Eval" line item that already exists (Retell's $0.10/min QA add-on is the existence proof). Typical ACV: $40k–$150k year 1 (per-locale rubric license + per-eval consumption).
- **Champion:** the AI-eng IC who lost a sleepless week last quarter chasing a Japanese-customer escalation triggered by a model swap. They want a CI gate that prevents the next one.
- **ICP test:** the vendor has ≥3 paying enterprise customers in JP/FR/DACH/LATAM, OR is responding to ≥1 active RFP that includes a "multilingual quality assurance" line item, OR has had a public quality incident in a non-English locale within 6 months.
- **Anti-customer:** end-customer enterprise buying voice-AI deployment QA for their *own* BPO floor — that's Cresta/Observe.AI's lane. We sell to the people who *build the agent*, not the people who *operate calls with it*.

## Wedge / where we could enter

The narrowest first move is **"Japanese-keigo CI gate"** — one rubric, one corpus, one obvious buyer set.

- **Candidate A — Japanese keigo regression suite for English-headquartered voice-AI vendors targeting JP enterprise.** The most asymmetric founder leverage; the vendors are the easiest cold-outbound list (Retell, Vapi, Synthflow, Bland, Replicant) and they all have the same RFP problem in Japan. Ship one rubric extremely well, get logos.
- **Candidate B — French-formality rubric for European voice-AI deployments.** Similar shape, different language, different vendors (Diabolocom, Vocapia in addition to the US incumbents). Adds a second locale and proves the model is not JP-only.
- **Candidate C — Code-switching rubric for US-Hispanic and Quebecois bilingual deployments.** Largest English-adjacent market; harder to differentiate against Cresta given they already sell into US healthcare payors with multilingual lines.

**What pushes us toward A:** keigo register is the single hardest cultural-linguistic test in the OECD, the founder's leverage is maximal there, the buyer pain is acute right now (April 2026 X discourse), and shipping one locale brilliantly is a stronger reference for B and C than shipping three locales adequately.

## What makes it defensible

- **(a) Primary: the calibrated multilingual rubric corpus.** Each rubric (keigo register, French formality, code-switching latency, etc.) is anchored by a native-speaker calibration set that gets richer with every customer's traffic and every model swap regression. The corpus compounds with engagements; an LLM-as-judge prompt without the calibration set is a vibes machine. Replicating this requires either (i) hiring linguists in three locales or (ii) buying us.
- **(b) Secondary: CI-native distribution into the vendor.** Once the vendor's deploy pipeline blocks on a Mensho check, ripping us out costs them their procurement story for the locale. The integration is sticky in the way every CI gate is sticky.
- **(c) Year-3 endgame: the cross-vendor benchmark.** If 6 of the top 10 voice-AI vendors run their JP/FR rubric through us, we are the de-facto multilingual leaderboard the AI-eng community references. That's a Braintrust-shaped position with cultural-rubric depth as the moat — and the leaderboard becomes the inbound channel for new buyers (vendors who don't want to be missing from it).

## How it could make money

| Layer | Price range | Comparable |
|---|---|---|
| **Layer 1 — Per-locale rubric license + calibration set** | $30k–$60k/yr per locale | [Braintrust Pro $249/mo + scoring overage](https://www.braintrust.dev/pricing) |
| **Layer 2 — Per-eval consumption (CI runs + production sample QA)** | $0.08–$0.15/min | [Retell AI Quality Assurance $0.10/min add-on](https://www.retellai.com/pricing) |
| **Layer 3 (later) — Cross-vendor benchmark / leaderboard sponsorships + insights** | $50k–$200k/yr | [Patronus FinanceBench-class benchmarks](https://patronus.ai/) |

Layer 1 is the wedge: the rubric license is what the AI-eng lead expenses today; the corpus and calibration set is what they cannot build internally without hiring linguists in Tokyo / Paris / Mexico City. Layer 2 echoes Levie's "consumption for agents" pricing thesis ([@levie on consumption pricing, 2026-04-18](https://x.com/levie/status/2045355693050655048)) — when each agent CI run scores N calls, per-eval pricing aligns price to value generated. Layer 3 is the reflexive endgame.

**Honest caveat on business-model risk.** The locale-by-locale services component of building rubrics will look services-flavored in year 1; the productization is real (the rubric, calibration set, and CI integration are reusable across customers in a locale) but the first three customers per locale will require hand-built corpus work. Acceptable as a wedge; ugly if we never escape it.

## What would pressure the thesis

1. **Assumption: voice-AI vendors will buy a third-party multilingual eval rather than building it in-house.**
   - **What would pressure it:** Retell or Vapi ships a "multilingual QA" SKU within 12 months that includes JP/FR rubrics. Or PolyAI's enterprise-tier "regional variants and code-switching" expands into a productized self-serve add-on.
   - **Lever:** position as the rubric authoring tool the vendor's eval team uses *internally*; sell the corpus and calibration sets rather than competing on the eval engine. Cede engine to vendors, keep the rubric+corpus.
2. **Assumption: cultural-linguistic regression is severe enough to block deploys, not just to log warnings.**
   - **What would pressure it:** vendors run our suite, see the regressions, and ship anyway because their procurement teams accept "improving over time" as the answer.
   - **Lever:** focus first wedge on customers with active RFPs requiring quality SLAs in non-English locales — i.e., regulated buyers (healthcare payors, banks) where a single insulting call is escalation-level. Drop the "general voice-AI vendor" pitch.
3. **Assumption: native-speaker calibration sets are a real moat against an LLM-as-judge with strong multilingual base models.**
   - **What would pressure it:** GPT-5.4 or Gemini 4 grades keigo register at human-linguist parity from a 5-shot prompt with no calibration set, making the corpus thin.
   - **Lever:** shift moat from corpus to **measurement methodology** — calibration against revealed-preference signals from customer escalations, NPS, and rejection logs. Tie our scores to real outcomes the customer already collects, not to a graded rubric the LLM might saturate.
4. **Assumption: Japanese voice-AI vendors don't displace the US-headquartered ones we sell to.**
   - **What would pressure it:** RevComm or a NTT-affiliated voice-AI stack wins the JP market, leaving our US-vendor wedge with no JP traffic to evaluate.
   - **Lever:** the rubric is portable. Pivot to selling the rubric license to MiiTel/RevComm directly — but then the founder-fit story (multi-market trilingual operator) gets tested against a single-market JP vendor's preference for a domestic supplier.

## 2-week experiment

**Load-bearing assumption to test:** voice-AI vendors with active JP customers will pay for a productized keigo-regression eval if shown a working scorecard on their own production agent.

**Artifact to build (week 1) — the *Mensho Keigo Scorecard v0*.** A public, hosted scorecard at `mensho.eval/keigo` that runs a curated 200-call Japanese-customer-service eval set (10 register dimensions × 20 scenarios, native-speaker-calibrated by 2 linguists Vincent contracts) against five publicly-accessible voice-AI vendor demo bots. Scores are visible per vendor; methodology is visible. The eval runs on Vincent's own infra (LiteLLM + a thin scoring harness; ~5 working days to ship as a Vincent-solo build using coding agents). When a vendor changes a model, we re-run and post the diff. Public Twitter announcement at launch ("here's how the top 5 voice-AI vendors handle Japanese keigo today").

**Conversations (week 2).** Target 8 voice-AI vendor AI-eng / VP-Eng leads — 5 from the publicly scored set (we already have a hook: their vendor is on the leaderboard) + 3 from vendors not yet on it (we offer to add them). Conversations open with the live scorecard on screen; we ask them to react to where their bot landed and what they'd change.

**Specific questions / asks** *(asked while the buyer is looking at the scorecard)*:
1. What's wrong about how we scored your agent? (Forces engagement with the rubric.)
2. If we sold this as a CI gate that ran on every model swap, what would your team pay per locale?
3. Would your procurement team accept a Mensho-graded scorecard as part of an RFP response in JP?
4. Who else inside your company would care about this score landing where it did?

**Pass criteria:** ≥3 LOIs from voice-AI vendor companies AND ≥1 vendor pulls forward a paid pilot with a stated PO date AND scorecard reaches ≥1k unique views with ≥3 inbound vendor requests to be added.

**Kill criteria:** <2 LOIs, vendors uniformly say "we'll build this internally next quarter" with no escalation interest, OR the scorecard fails to differentiate vendors meaningfully (i.e., they all score similarly enough that the regression-test framing has no teeth).

**Vincent's effort.** ~30 hours build (corpus + harness + public site), ~25 hours linguist coordination and corpus QA, ~20 hours conversations and writeup. Output: the public scorecard URL, a memo with quoted answers from the 8 conversations, a go / pivot / kill recommendation.

## What we don't know yet

- Whether voice-AI vendors will share production call samples with a third party for CI evaluation, or whether they'll only run synthetic test sets (changes the value prop and the corpus economics).
- Whether the keigo rubric generalizes across vendor stacks cleanly, or whether each voice/STT/TTS combo creates idiosyncratic failure modes that need per-stack rubric tuning.
- Whether "multilingual QA" actually shows up as a distinct line item in voice-AI procurement RFPs today, or is folded into "quality" generically — affects how concretely we can position the wedge.
- Whether the linguist-network supply chain is durable at scale (10+ locales) or whether the model collapses past 3.

## Vincent's Feedback

**Disposition: pass on this wedge.** The surrounding pieces are real — founder-fit (trilingual EN/FR/JA + Amazon evals + linguist network), procurement-defensibility motivation, CI-gate distribution play, leaderboard endgame — but the wedge as drafted has three load-bearing problems that compound.

1. **Scope ambiguity across the voice stack.** Unclear whether Mensho evaluates the LLM that produces the text (then handed to TTS), the TTS itself, or ASR/STT. The draft mixes signals from all three: keigo register / *teineigo-sonkeigo-kenjōgo* mix / tu-vous switching read like text-LLM evals; "intonation that sounded like a Chinese accent" and "voice that says *moushiwake gozaimasen* at the right register" read like TTS prosody evals; *aizuchi* timing and code-switching latency are pipeline-level. The wedge can't be all three at once — buyer, corpus, and tech stack are different for each.
2. **Layer mismatch between demand signal and product.** The viral incidents the proto cites as proof of pain (the X "Chinese-accent intonation" thread, the "creepy processing pauses" complaint) are *audio-layer* failures. The rubric the proto actually describes is *text-LLM-judgeable* (register accuracy, formality switching, untranslated-term policy). A text-register eval, even done extremely well, would not have caught either failure mode the proto uses to justify its existence. Product and demand are pointing at different layers of the stack.
3. **Differentiation gap with a structural clock.** The elevator pitch reads like generic LLM-eval (Braintrust, LangSmith, Patronus all support custom rubrics + LLM-as-judge today) plus Japanese prompts. The "native-speaker calibration corpus" moat lives in the defensibility section, but pressure-test #3 names the structural risk honestly — frontier multilingual models will likely grade keigo at near-linguist parity from a 5-shot prompt within the bet's horizon, eroding the corpus moat. The proposed lever ("shift moat to revealed-preference signals from customer escalations") is hand-wavy and arguably converts the product into customer-feedback analytics, with a different buyer.

**Adjacent space worth noting: TTS-prosody quality eval for non-English locales.** Off-the-shelf LLM-as-judge cannot grade audio, the failure mode matches the demand signal the proto cited, and the native-speaker linguist network would be genuinely load-bearing for MOS-style ground truth. Different bet from this one — different buyer (TTS vendors / vertical voice-app builders rather than agent vendors), different tech stack — but the founder-fit overlaps. Carrying forward as a possible direction, not as a pivot of this proto.

## Related

- [[Banto — Voice-first generative interface that turns a Japanese ryokan's own service standards into a per-shift operating system for the floor]]
- [[Bellwether — private on-prem eval harness for enterprise coding-agent fleets]]
- [[Touchstone — Per-variant evals so the bespoke-software era doesn't ship a million silently-wrong internal tools]]
- [[Tessera — Fit-confidence API for agent-mediated apparel commerce trained on smart-glasses body capture]]
