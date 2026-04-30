---
proto_generator:
  seed: 846313158
  writer: 1
  writers_total: 3
  repo_sha: 7c0132d
  generated_at: 2026-04-30T09:03:41+00:00
id: proto-banto
aliases:
  - Banto
tags:
  - proto
type: proto
status: drafted
created: 2026-04-30
origin: ""
---

# Banto — Voice-first generative interface that turns a Japanese ryokan's own service standards into a per-shift operating system for the floor

## What is it?

**Elevator pitch**: A Japanese ryokan or boutique hotel uploads its existing service manuals, room-cleaning standards, and shift handover notes; in return, every floor staff member gets a voice-first phone app that listens to them through a discreet earpiece while they work, generates the right checklist or task screen for what they're actually doing right now, and absorbs each shift's friction back into the manual. The owner-operator stops losing their service standard every time a staff member quits.

**How it works**: The buyer plugs in their own artifacts — service manuals (often a Word doc plus tribal memory), housekeeping standards, the *okami's* handover notebook, the daily reservation sheet from their PMS. We ingest these into a per-property knowledge base. Each staff member wears a bone-conduction earpiece tied to their phone. They speak in Japanese to log a guest preference, ask "next room?" mid-turnover, or flag a maintenance issue; Whisper transcribes, a small reasoning model resolves intent against the property's standards and current floor state, and the phone renders a screen built for *this* worker doing *this* task right now (not a one-size-fits-all dashboard). Manager-grade output — what slipped, who needs coaching, what to add to the manual — falls out as a byproduct.

## What's the problem?

Owner-operators of Japanese inns and boutique hotels are losing their service standard one resignation at a time. They run a multi-room operation on a thinning crew, often supplemented by Specified-Skilled-Worker (SSW) visa holders whose Japanese is intermediate. The *okami* (proprietress) used to walk the floor and correct on the fly; now she's running reception too. The institutional knowledge — which guest disliked tatami, which room's *kakejiku* is fragile, which towel goes where — sits in her head, in a binder, and in handover notes that get forgotten between shifts. Existing software (PMS, channel managers) tracks bookings, not service standards. So omotenashi quietly degrades, repeat-guest rates slip, and TripAdvisor scores follow.

## Why now (2026)

- **Japan is set to face the largest tourism-labor shortfall of any country studied — a projected 29% gap by 2035 — in the same decade its visitor base has just blown past 39 million arrivals (11 months of 2025 already eclipsed the previous annual record)** ([Japan Times on WTTC report](https://www.japantimes.co.jp/business/2025/10/10/toursim-labor-shortage/), [JNTO via Travel Voice](https://www.travelvoice.jp/english/international-arrivals-in-japan-reached-39-million-in-total-with-3-5-million-in-november-2025-already-breaking-the-previous-annual-record)). The labor and demand curves are already crossing.
- **85% of travel and hospitality operators in Japan have already been forced to limit operations due to labor shortage** — 51% reduce operating days, 33% shorten hours, 27% reduce rooms-for-sale ([Travel Voice on STU survey](https://www.travelvoice.jp/english/85-of-travel-and-hospitality-business-operators-in-japan-are-forced-to-limit-their-operation-hours-due-to-labour-shortage)). The buyer is no longer choosing between margin and service quality; they're choosing between staying open and not.
- **Voice STT supports Japanese natively.** OpenAI's Whisper README ships Japanese as a first-class supported language with a documented `whisper japanese.wav --language Japanese` command and a published per-language WER/CER breakdown ([OpenAI Whisper repo](https://github.com/openai/whisper)). A floor worker can talk, not type.
- **Generative UI has crossed from research demo to YC thesis.** YC's Summer 2026 RFS explicitly calls out "Dynamic Software Interfaces" — the bet that coding agents are good enough that *users* (or, here, *operators*) become their own forward-deployed engineers and software ships shared primitives that get composed per-context ([YC RFS](https://www.ycombinator.com/rfs)). A floor worker mid-turnover and a night-shift front-desk clerk shouldn't see the same screen.
- **Existing hospitality SaaS is built for desks, not floors.** Even the dominant operations platform — Amadeus HotSOS, deployed at properties like the Hotel Okura — is a tablet/phone task-list and ticket queue for staff, with a "modern interface" upgrade as its 2025 headline feature ([Amadeus HotSOS](https://www.amadeus-hospitality.com/service-optimization-software/hotsos/)). It is not voice-first, not generative, and not designed around encoding the property's *own* service standards.

## Who else is doing this

- **Guest-facing hospitality voice AI** — main player: **[Aiello](https://aiello.ai/)** (voice-AI for hotels, with named deployments at IHG and MHR). Adjacent: **[Kotozna](https://www.kotozna.com/en/)** ("managing multilingual experiences for 500+ global tourism clients" — generative-AI chatbot/concierge for tourism). Both are *guest-facing concierge* products — they reduce front-desk inbound volume; they don't help the housekeeper, kitchen runner, or floor lead deliver the property's service standard.
- **Hotel operations / staff task platforms** — main player: **[Amadeus HotSOS](https://www.amadeus-hospitality.com/service-optimization-software/hotsos/)** (mobile task tickets, multilingual, with named deployments at Hotel Okura and Fattal Hotels across 38 properties). These are work-order routing systems: a guest asks for towels, ticket fires, housekeeper acknowledges. They do not encode standards-of-service, do not adapt the interface per role/task, and are not voice-first.
- **Voice-first dictation / agent input** — main player: **[Wispr Flow](https://wisprflow.ai/pricing)** ($15/user/mo Pro, voice dictation with command mode for editing). Horizontal voice input — doesn't know what a ryokan is, doesn't ingest service manuals, doesn't generate workflows.

**Where the opening is.** Every category above owns one slice — guest-side voice, ticket routing, generic dictation. None of them takes the *operator's own service standard* as the primary input and renders a per-worker, per-task interface against the live floor. The legacy ops vendors won't do this — Amadeus's headline HotSOS update is positioned as a "New, More Intuitive Experience" (see the [HotSOS page](https://www.amadeus-hospitality.com/service-optimization-software/hotsos/)), not generative interfaces, and their distribution motor is GM-down enterprise sales, not the SSW housekeeper at a 30-room ryokan in Hakone. The guest-facing voice AIs would have to abandon their inbound-tourism narrative to pivot inward to staff. The opening is a Japan-first, staff-floor, voice-first product that an owner-operator buys because their *own* service standard becomes durable infrastructure rather than a binder no one reads.

## Why us

- **Vincent has working familiarity with Japanese institutional culture and language**, plus French/Canadian/US frames to read what an outside-built SaaS misunderstands about how a ryokan actually runs. The horizontal incumbents do not have a partner who can sit through a service-handover meeting in Hakone and read the room.
- **End-to-end agentic build experience** means an MVP — voice-in, manual-ingest, generative-task-screen-out — is a Vincent-solo build, not a "raise to hire 10 engineers" build.

## Customer & buyer

- **Customer:** floor staff (housekeeping lead, *nakai-san*, front-desk clerk, F&B server) at independent or small-chain Japanese ryokan and boutique hotels (10–80 rooms).
- **Buyer:** the *okami*, owner-GM, or COO at a small ryokan group. Budget line: operations / staff productivity. Typical ACV target: ¥30–80k/month per property at first wedge.
- **Champion:** the *okami* or head housekeeper — the person whose head currently holds the service standard and who feels every degradation personally.
- **ICP test:** independent or 2–10-property operator with ≥1 SSW visa hire on staff in the last 12 months, an existing Word/PDF service manual, and self-reported staff turnover ≥20%/year. Three of three.
- **Anti-customer:** large branded chains (Hilton, Marriott Japan) with corporate IT and an Amadeus contract — too long a sales cycle, too much policy override; and *minshuku*/Airbnb-scale (1–4 rooms) where the operator is the staff and the binder is in their head.

## Wedge / where we could enter

- **Candidate A — Housekeeping/turnover voice copilot.** Pure ops focus: voice-driven turnover checklists generated from the property's housekeeping standards, with photo capture for damage. Easiest to demo, lowest customer risk, but smallest standalone willingness-to-pay.
- **Candidate B — Shift handover capture.** Replace the *okami's* handover notebook: the night manager talks for 90 seconds at end-of-shift, system extracts guest-state deltas, generates the morning briefing tailored to each role on shift. Highest emotional pull for the buyer (it's literally her notebook); narrower initial surface area.
- **Candidate C — Multilingual floor coach for SSW staff.** Earpiece prompts for SSW housekeepers with limited Japanese, in their language; standards stay in Japanese. Highest social-impact framing; risk that the buyer reads it as "training" not "operations."

What pushes us to one: pilot conversation with 5 ryokan in Hakone/Kyoto reveals which pain the *okami* describes first, unprompted, in the first 10 minutes. Lean toward (B) if she opens with handover; (A) if she opens with cleaning quality; (C) if she opens with the SSW Japanese gap.

## What makes it defensible

- **(a) Primary — encoded service standards as a per-property knowledge graph.** Each property's manual, tribal memory, and shift-by-shift corrections accrete into a structured representation no competitor can clone without spending the same months in the same property. Switching cost is the binder you no longer maintain anywhere else.
- **(b) Secondary — Japan-first distribution and trust.** Selling into independent ryokan requires showing up, speaking the language, understanding *kao* (face) and *nemawashi* (consensus-building). A Tokyo-based operation with French-Canadian connective tissue to the West has an unfair advantage over a US horizontal that lands a Japan AE in year three.
- **(c) Year-3 endgame — the labels for service quality.** Once 200+ properties are running on this, the corpus of "what good service looks like" — across rooms, seasons, guest types — becomes training data for a Japanese-hospitality-tuned model that nobody else can assemble. The validated feedback pattern from prior protos: use the user's own existing artifacts (the manual + the daily corrections) as the labeled training set.

## How it could make money

| Layer | Price range | Comparable |
| --- | --- | --- |
| **Layer 1 — Voice + generative-UI floor app** | ¥1,500–2,500/user/mo (~$10–17) | [Wispr Flow Pro](https://wisprflow.ai/pricing) at $15/user/mo for horizontal voice input |
| **Layer 2 — Per-property service-standard knowledge layer** | ¥30k–80k/mo per property | [Amadeus HotSOS](https://www.amadeus-hospitality.com/service-optimization-software/hotsos/) (per-property enterprise SaaS for hotel operations; pricing not public) |
| **Layer 3 (later) — Multi-property analytics + benchmarking for small chains** | ¥150k–400k/mo per group | Same enterprise-tier comparable |

Honest caveat: services-trap risk is real. Onboarding a property means parsing their manual and sitting through a handover with the *okami*; if the per-property setup cost stays >2 weeks of human time, unit economics break at the 10-property mark. Test early whether 80% of the ingest can run unattended on the manual + a 1hr Zoom.

## What would pressure the thesis

1. **Assumption:** the *okami* / owner-operator will *trust* a voice-first AI on their floor enough to put it between her and her staff.
   - **What would pressure it:** in the 2-week experiment, ≥3 of 5 conversations end with "interesting, but I'd want to wait until [chain X] uses it." That's a trust-not-product objection and Japan-specific.
   - **Lever:** lead with a single Hakone or Kyoto lighthouse (a respected *ryokan kumiai* member) and treat year 1 as an apprentice/testimonial-building operation, not a sales-funnel operation.
2. **Assumption:** the per-property service standard is rich enough to generate useful interfaces *without* per-property fine-tuning. Generic prompts + ingested manual is enough.
   - **What would pressure it:** the v0 generative UI looks the same across the first three properties because the manual ingest produces a lowest-common-denominator schema.
   - **Lever:** narrow to one scenario (turnover, or handover) and ship depth, not breadth, until per-property differentiation is visible.
3. **Assumption:** Aiello, Kotozna, or HotSOS will not pivot inward to staff-floor-with-voice within 18 months and squeeze us out.
   - **What would pressure it:** Aiello announces a "staff app" or HotSOS announces a generative-UI mode at HITEC Tokyo (Dec 2026).
   - **Lever:** the per-property service-standard graph is the moat — keep the pace of property onboarding ahead of any incumbent's distribution-into-independent-ryokan motion, where they are weakest.
4. **Assumption:** SSW labor inflow continues and creates the multilingual coaching wedge.
   - **What would pressure it:** Japan tightens the SSW Accommodation visa or the language-screening rules currently being floated cut intake materially.
   - **Lever:** the bet does not require SSW to work — it just makes the wedge more expansive. Fall back to Japanese-only handover/turnover if SSW supply tightens.

## 2-week experiment

**Load-bearing assumption to test:** an owner-operator *okami* will, after seeing a working voice-driven turnover demo grounded in her own service manual, agree to a 4-week paid pilot at her property — i.e., she trusts the artifact enough to let it onto her floor.

**Artifact to build (week 1):** a working v0 of the housekeeping turnover loop. Vincent solo, ~5 working days using coding agents:
- Take a real ryokan service manual (synthetic / public-template if no design partner yet) and ingest it into a per-property knowledge base.
- Bone-conduction earpiece + iOS PWA. Worker says "starting room 204"; Whisper transcribes; the screen renders the property-specific turnover checklist for that room category, with photo-capture for damage and a "next?" voice command.
- Backend: a 3-minute screencast of the *okami*-view — what got flagged across the shift, what to add to the manual.
- Hosted publicly with a 90-second walkthrough video in Japanese (with English subtitles) on a single landing page.

**Conversations (week 2):** 6–8 *okami* / owner-GMs at independent ryokan and boutique hotels in Hakone, Kyoto, and Kanazawa. Sourced via the *Ryokan Kumiai* (industry association), warm intros from JETRO contacts, and direct cold outreach. Each conversation opens with the artifact running on a phone, *not* a deck. Vincent travels.

**Specific questions / asks** (each answerable in 30 minutes with the artifact in hand):
1. "If your senior housekeeper retired tomorrow, where in this artifact would the gap show up first?"
2. "Show me the handover notebook you keep right now — what's in it that this doesn't capture?"
3. "Would you let your SSW housekeepers wear the earpiece in a guest-facing room during peak season? What would have to be true?"
4. "What's the maximum you'd pay per month per property for this if it actually held your standard for 90 days?"
5. "Which of your peer ryokan would be the worst possible reference if it leaked? Which would be the best?"

**Pass criteria**: ≥3 signed paid-pilot LOIs (¥30k+/mo per property, 90-day commit) AND ≥1 buyer names a specific cohort of peer ryokan she'd refer AND the screencast gets ≥30 inbound from independent operators (LINE, email, IG DM).

**Kill criteria**: <2 LOIs after 8 conversations OR every *okami* defaults to "let's wait until [chain] uses this" (the trust-not-product objection from Pressure-Test #1).

**Vincent's effort**: ~80 hours total. Build: ~40h (coding agents do the bulk of the PWA/STT pipeline). Conversations: ~25h including Japan travel. Synthesis & memo: ~15h. Output: hosted artifact + LOIs + memo with verbatim *okami* quotes + go / pivot / kill recommendation.

## What we don't know yet

- Whether bone-conduction earpieces are culturally acceptable on the ryokan floor in front of guests, or whether the form-factor needs to be invisible (collar mic, neck-loop) in year 1.
- Whether the *Ryokan Kumiai* / regional industry associations will become a distribution channel or a gatekeeper-blocker.
- The right pricing anchor in JPY for a small independent ryokan that has never paid for SaaS beyond their PMS — is the binary "yes/no at any price" or is there elasticity in the ¥10k–80k band?
- Whether the same product (manual-ingest + voice + generative UI for service standards) generalizes to non-Japan hospitality in years 2–3, or whether the Japanese-cultural specificity is the moat *and* the ceiling.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Genba — Productized agent-fleet enablement program for Japanese engineering teams]]
- [[Torii — Consent and residency gateway for foreign agents calling Japanese enterprise APIs]]
- [[Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses]]
