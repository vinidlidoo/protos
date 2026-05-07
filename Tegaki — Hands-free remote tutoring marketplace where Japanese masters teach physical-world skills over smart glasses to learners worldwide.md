---
id: proto-tegaki
aliases:
  - Tegaki
tags:
  - proto
type: proto
status: drafted
created: 2026-05-06
origin: ad-hoc-seeded run, seed 541947910
proto_generator:
  seed: 541947910
  writer_index: 1
  repo_sha: 1d05c7b8a4022c970e37d7886e1ba37e5ad12679
  generated_at: 2026-05-06T23:35:27Z
  mode: ad-hoc-seeded
---

# Tegaki — Hands-free remote tutoring marketplace where Japanese masters teach physical-world skills over smart glasses to learners worldwide

## What is it?

**Elevator pitch.** Learners outside Japan strap on smart glasses, press one button, and a Japanese master appears in their ear — watching their hands through the glasses' first-person camera, correcting their grip, angle, and pressure in real time over voice, with live translation collapsing the language barrier in both directions. The first vertical is bonsai, where Western enthusiasts already pay Japan-trained pros hundreds of dollars per day for in-person workshops they can rarely access; the platform makes that lesson a $60–120 booking from your backyard.

**How it works.** A learner books a slot from a Japan-resident master listed on Tegaki. At lesson time both parties join through a glasses-aware app: the learner streams first-person video + audio from a supported display-class wearable (Meta Ray-Ban Display [$799 since Sept 30, 2025](https://www.meta.com/blog/meta-ray-ban-display-ai-glasses-connect-2025), Mentra Live, Snap Spectacles), the master sees the feed on a tablet and speaks in Japanese; the learner hears English/French/etc. via on-device translation; the master sees subtitled questions back. Every lesson is recorded with both-party consent — first-person video of the learner's hands, master's spoken corrections, and a follow-up outcome photo a week or month later. That triple becomes the labeled training corpus that, over years, lets the platform ship AI-augmented coaching alongside the human master, then eventually an AI tutor for entry-level lessons the human masters no longer want to teach.

## What's the problem?

Western enthusiasts who want to learn a Japanese craft from a Japanese master have three bad options: travel to Japan for a week-long workshop (expensive, rare, language-gated); hope a touring master visits their city once every few years; or settle for pre-recorded YouTube videos where the camera is in the wrong place — pointed at the master's hands, not the student's, so the student never learns whether *their* angle is right. The diagnostic moment in any physical-skill lesson is "let me see what you're doing wrong" — and that moment requires the teacher to see the student's hands. Smart glasses finally put that camera in the right place.

## Why now (2026)

- **Display-class smart glasses are now a real consumer category, not a developer kit.** Meta Ray-Ban Display launched September 30, 2025 at $799 including the Neural Band, with in-lens display, live captions and translation built into the OS, and demos booked out through mid-October at launch [meta.com](https://www.meta.com/blog/meta-ray-ban-display-ai-glasses-connect-2025). A first-party, fashion-grade device with a translation feature on its launch-week feature list is the unlock — five years ago this category was Hololens-shaped and unwearable.
- **An open smart-glasses ecosystem now exists alongside Meta's walled garden, lowering integration risk.** Mentra raised US$8M in seed funding in July 2025 and shipped Mentra Live with an open MentraOS and a third-party MiniApp Store, explicitly positioning against "closed and dominated by Big Tech" [eyesmart.com.au](https://eyesmart.com.au/newsarticle/7417-mentra-launches-first-smart-glasses-with-dedicated-app-store). A consumer-glasses app no longer needs Meta's permission to ship, which means a tutoring app can be a first-class glasses experience by 2027.
- **Live speech-to-speech translation crossed the "good enough for casual conversation" bar in 2026.** Google Translate's "Live Translate," powered by Gemini, launched in Japan on March 27, 2026 with 70+ language real-time support running on iOS [gemilab.net](https://gemilab.net/en/articles/gemini-updates/google-translate-live-translate-japan-gemini-ai). Conversational JA↔EN translation is now a commodity on a phone in your pocket — the remaining gap (craft-jargon, dialect, register) is exactly where a vertical product can build proprietary glossaries.
- **Proof-of-humanity infrastructure is unusually well-deployed in Japan, making "verified-human master" a first-day feature, not a roadmap item.** As of August 2025, World partnered with Medirom to install iris-scanning Orbs in Japan's Re.Ra.Ku salon chain, targeting 100 salons by year-end and 500,000 new World IDs annually from salon visitors [biometricupdate.com](https://www.biometricupdate.com/202508/world-partners-with-japanese-relaxation-brand-to-deploy-biometric-orbs). Japan is one of very few countries where a Japan-resident master can plausibly walk to a nearby orb and be verified this year.
- **Tradesperson-grade first-person capture on Meta Ray-Ban is already happening — the workflow exists outside our category.** The founder of Tradeye, building egocentric datasets for embodied AI, reports that smart-glasses adoption among working tradespeople is "relatively easy" because the form factor reads as normal safety eyewear on jobsites [x.com/TradeyeLLC](https://x.com/i/status/2051480153579249751). The capture habit is forming in adjacent skilled trades right now.

## Who else is doing this

- **Industrial AR remote-assist platforms** — main player: **[Help Lightning](https://helplightning.com/solutions/solutions-overview/)**, with patented merged-reality video collaboration and certified support for Vuzix, RealWear, Epson, Lenovo and Zebra glasses. Others: [Augmentir](https://www.augmentir.com/pricing) (connected-worker platform with Remote Assist for manufacturing), [TeamViewer Frontline](https://www.teamviewer.com/en/products/frontline/). They sell into Fortune-500 field-service org charts, not consumers; the buyer is a VP of Service writing a six-figure ARR check, not an enthusiast booking a single $90 lesson.
- **Subscription craft-education libraries with Japan-trained masters** — main player: **[Bonsai Mirai](https://live.bonsaimirai.com/)**, founded by Ryan Neil (a full Japanese-apprenticeship graduate under Masahiko Kimura), with 600+ videos / 800+ hours of recorded instruction, 17 instructors, members in 52 countries, priced $9.99 / $17.99 / $29.99 per month [live.bonsaimirai.com/pricing](https://live.bonsaimirai.com/pricing). It is the closest analog and a strong proof of demand — but it is recorded video plus a forum, with no live first-person feedback loop and no Japan-resident master roster.
- **Online language and skill marketplaces with Japan-resident teachers** — main player: **[italki](https://www.italki.com/en/blog/japanese-tutor-cost)** with online Japanese lessons typically $15–$50/hr (italki listings start from $4). Others: [Cafetalk](https://cafetalk.com/tutor/page/payment/?lang=en) (the dominant Japan-domestic lesson marketplace, paying tutors a 60% margin that rises to 70% after sustained activity); [Preply](https://preply.com/). They sell phone-camera or webcam lessons; none ship a glasses-native first-person tutoring experience and none specialize in physical-craft instruction.
- **Live-class platforms that already pay independent teachers at scale** — main player: **[Outschool](https://exa.ai/library/company/outschool)**, a kids-focused live small-group platform with 1,143 employees that contracts independent teachers to deliver classes via live video. Pattern-of-life proof that "people book live small-group online sessions with vetted independent teachers" is a category, not a hypothesis — but the buyer is a parent and the format is webcam, not glasses.

**Where the opening is.** Industrial AR remote-assist has built the technical playbook for "expert sees what the field worker sees" but priced and packaged it for enterprise field-service buyers; it will not cross the chasm into a consumer marketplace because the GTM, pricing, and support model are wrong for a $90 booking. Subscription craft libraries like Bonsai Mirai have proven craft enthusiasts will pay monthly for Japan-trained instruction but have no live feedback and no Japan-resident roster. Language and skill marketplaces have the marketplace mechanics but treat the tutoring session as a webcam call, not a first-person hands-on apprenticeship. The opening is a vertically-integrated marketplace whose product is glasses-native from day one, whose roster is Japan-resident, and whose lessons compound into a recorded-skill corpus no horizontal player will assemble.

## Why us

- **Three-language, three-continent operator with a decade in Japan.** Sourcing the first 50 Japan-resident masters is a network problem in Japanese, the first 5,000 international learners is a marketing problem in English and French, and contract reconciliation across both is a translation problem. Vincent has shipped products inside the largest two-sided marketplace on Earth (Amazon Fashion, 5y) and has the cultural fluency to negotiate with iemoto-structured guilds rather than around them.
- **Direct experience evaluating ASR and translation models at production scale.** Audio-acoustic quality during a craft-jargon-dense lesson is the load-bearing technical risk. Vincent led AI model evaluations at Amazon, including specialized work on ASR and audio — exactly the regression-testing skill set the prosody / register / domain-vocabulary translation problem demands.

## Customer & buyer

- **Customer:** intermediate-to-advanced bonsai practitioner (≥2 years of practice, ≥5 trees in cultivation), 35–60, US/EU/AU, with a stated preference for Japanese technique. The same role is the buyer — these are individual hobbyists with discretionary craft budgets in the low thousands per year.
- **Buyer:** the same person; a $60–120 lesson is a personal-credit-card decision, not a procurement event.
- **Champion:** local bonsai-club leaders (US: ~250 ABS-affiliated clubs; EU: EBA federations) who already organize "visiting Japanese master" workshops once or twice a year. They become unpaid distribution if the platform makes their members' between-workshops practice better.
- **ICP test:** owns ≥1 collected (yamadori or pre-bonsai) tree they consider "important," has paid ≥$300 for at least one in-person workshop in the last 24 months, and has previously asked a question on a forum where the top-voted answer was "you really need to ask a Japanese teacher."
- **Anti-customer:** absolute beginners with mall-bought juniper "starter kits." Bonsai Mirai's recorded-video offering serves them better at $9.99/month and their lesson signal-to-noise ratio is too low for the recorded-corpus moat.

## Wedge / where we could enter

The narrowest first move is **bonsai consultations**, specifically *single-tree styling reviews* with a Japan-resident master who has at least 5 years' apprenticeship under a recognized teacher. One tree, 60 minutes, the learner brings questions and the tree to their workbench, the master watches over the glasses and corrects branch selection, wire angle, and movement. Same-week follow-up photo from the learner, attached to the lesson record.

- **Candidate A — Single-tree styling review.** $80–120, 60 min, primary launch SKU. Highest WTP, clearest outcome label, easiest for a master to deliver.
- **Candidate B — Seasonal-care diagnostic call.** $40–60, 30 min, "is this tree healthy / what should I do this month." Lower WTP but higher session frequency, builds the calendar habit.
- **Candidate C — Multi-week mentorship arc.** $400–800 for 4 sessions over a season. Reserved for repeat customers; protects against churn after the curiosity-purchase first lesson.

Push toward A first because it's the SKU that produces the cleanest data triple (first-person video + master correction + follow-up photo) and the SKU most differentiated from Bonsai Mirai's recorded library.

## What makes it defensible

- **(a) Primary — supply-side network effects on a Japan-resident master roster that's hard to clone.** The first 30 masters are sourced through Japanese-language outreach into apprenticeship networks (Omiya, Kinashi, Shōhin Suzuki lineage). Each master who signs and earns ≥¥200k/month within 90 days becomes a recruitment engine for the next 5; an English-only competitor cannot reach this pool without hiring our exact team.
- **(b) Secondary — proprietary recorded-lesson corpus with outcome labels.** Each consenting lesson contributes (first-person video at hand-distance + master spoken corrections in JA + learner follow-up photo at T+30 days). After 10,000 lessons this is the only labeled "expert-corrects-novice" bonsai dataset in existence; it powers in-session AI assistance (auto-translation glossary, "the master cut a similar branch this way last month" callbacks) and, by year 4–5, an AI tutor for the seasonal-care SKU.
- **(c) Year-3 endgame — vertical-specific translation glossary that horizontal MT can't match.** Bonsai vocabulary (*jin*, *shari*, *uro*, *moyōgi*, *shakan*, *sabamiki*) is mistranslated by frontier MT today. A platform-internal glossary curated by paid masters is *the* feature that makes the lesson actually work, and it compounds with every lesson recorded. The same template re-runs in every subsequent vertical (sushi knife terminology, kintsugi lacquer terms, etc.).

**Honest layer-N caveat.** The "human tutors today, AI tutors tomorrow" trajectory is real but is a category change, not a moat extension. Today the company is a marketplace whose moat is supply-side network effects; in year 5 the AI tutor is a B2C software product whose moat is the data corpus. We do not paper over the transition: the marketplace must be defensible *as a marketplace* even if the AI-tutor leg never ships, because world-model maturity for embodied physical-skill tasks is genuinely uncertain on a 5-year horizon.

## How it could make money

| Layer                                                           | Price range              | Comparable                                                                                            |
| --------------------------------------------------------------- | ------------------------ | ----------------------------------------------------------------------------------------------------- |
| **Layer 1 — Marketplace take rate on live lessons**             | 25–35% of $60–120 lesson | [Cafetalk takes 30–40% (60–70% margin to tutor)](https://cafetalk.com/tutor/page/payment/?lang=en)    |
| **Layer 2 — Annual learner membership for AI assist + library** | $19–29 / month           | [Bonsai Mirai Standard $17.99 / Pro $29.99](https://live.bonsaimirai.com/pricing)                     |
| **Layer 3 (later) — AI tutor for seasonal-care SKU**            | $9–19 / month            | [Italki Saver / Outschool tutoring subscriptions](https://www.italki.com/en/blog/japanese-tutor-cost) |

Honest caveat: the marketplace cold-start is the canonical hard problem. The membership layer cannot be load-bearing at launch (no library yet); the AI-tutor layer is years out and depends on the corpus actually preserving the signal we need. For the first 18 months this is a take-rate-on-lessons business with a roughly $300–600 GMV/master/month assumption — meaning 100 active masters and 8% take is ~$240k–$480k ARR, not a venture-scale revenue line on its own. The bet is that the same operator skill and the same recorded corpus then unlock vertical 2 (sushi), vertical 3 (kintsugi), and so on — the marketplace is one of N before the membership and AI layers compound.

## What would pressure the thesis

1. **Assumption:** display-class smart glasses reach ≥5M global active users by end of 2027, enough to support a paid consumer category. *(Vincent's named dominant risk.)*
   - **What would pressure it:** Meta Ray-Ban Display sales below 500k units in its first full year and no second-tier OEM (Samsung, Apple, Google) shipping a competing display-class device by mid-2027. Persistent privacy backlash also pressures this: in April 2026 Meta cancelled its contract with Sama after Kenya-based annotators told Swedish newspapers they had reviewed Ray-Ban smart-glasses footage of users undressing and using the toilet — 1,108 workers were made redundant and UK and Kenyan regulators opened privacy inquiries [bbc.com](https://www.bbc.com/news/articles/c5y7yvgy0w6o). That is exactly the trust-collapse pattern that slows mainstream adoption.
   - **Lever:** ship a phone-camera fallback experience (handheld POV through a stand) so the marketplace works at degraded quality on existing iOS/Android, then upgrade users to glasses as adoption catches up. This protects the supply-side bootstrapping work even if the device curve slips a year.
2. **Assumption:** real-time translation quality is sufficient for technical craft instruction — not just casual conversation.
   - **What would pressure it:** masters consistently report the auto-translation mangles their corrections, learners systematically misunderstand cuts/wiring, lessons end with "I'm not sure what you wanted me to do." This is where the auditory/prosody/register problem bites — *which-branch* corrections are time-deictic and gesture-anchored in ways frontier MT does not handle.
   - **Lever:** build a vertical-specific bilingual glossary curated by paid masters (this is the year-3 moat; bring it forward) and add an explicit "confirm intent" UX beat where the learner repeats the action back in English and the master sees the back-translation before the cut.
3. **Assumption:** the recorded-session triple (first-person video + master audio + follow-up outcome photo) actually preserves the signal needed to train AI coaching and, eventually, an AI tutor.
   - **What would pressure it:** lessons end up dominated by chitchat audio, glasses-cam resolution at hand-distance is too low to resolve the wire-and-branch detail, the outcome photo arrives late or never. Industry signal here is real — Objectways scrapped 150–200 robotics-training videos for inconsistent recording and edge-case variability [x.com](https://x.com/i/status/2042955313188413563).
   - **Lever:** pay masters a small recording-quality bonus for sessions that pass an automated rubric (audio SNR, hand-distance focus, outcome photo on file at T+30) — the rubric becomes the data-quality contract.
4. **Assumption:** Japan-resident masters will record their craft and accept a 25–35% platform take.
   - **What would pressure it:** iemoto / guild structures explicitly forbid recorded lessons; masters demand 90% take given low Japanese consumer-tutoring rates; consent-to-record refusals exceed 30% of the supply pool.
   - **Lever:** open with masters who are already operating outside iemoto structures (Mirai-network expats, second-generation studios with English-speaking heirs); position consent-to-record as the option that unlocks the international rate ($80–120 vs domestic ¥3000–5000), making it self-selecting.

## 2-week experiment

**Load-bearing assumption to test:** *In a glasses-mediated, voice-translated lesson on a real bonsai tree, can a Japan-resident master actually deliver a styling correction that the learner can execute and that visibly improves the tree?* Everything else (marketplace mechanics, take rate, vertical expansion) is downstream of this single question working at acceptable quality.

**Artifact to build (week 1):** a working **[Tegaki demo lesson]** — a public 8-minute screencast plus a hosted single-page lesson-booking demo, where Vincent (wearing Meta Ray-Ban Display borrowed or rented) takes a real styling lesson on his own collected pre-bonsai from a Japan-resident master Vincent has paid out-of-pocket. The screencast splits into three quadrants: (1) first-person glasses view of Vincent's hands, (2) audio with Japanese original + live English translation captions overlaid, (3) the master's tablet view with subtitled questions back, and (4) before / after photos of the actual tree. The booking page is one-button, captures email + tree-photo upload, and routes to Vincent personally for the next 10 lessons. Build cost: 5 working days, mostly UI plumbing and consent/recording flow; the lesson itself is the demo.

**Conversations (week 2):** 12 named conversations — 5 with Bonsai Mirai Pro subscribers found through their forum (consumer demand-side), 4 with Japan-resident bonsai pros sourced through Vincent's Japan network and intro-asks at Omiya Bonsai Village (supply-side WTP for the take rate), 3 with bonsai-club leaders in the US/EU (distribution channel). Every conversation opens with the screencast playing in the first 90 seconds.

**Specific questions / asks:**
1. (To learners, with screencast running.) "Would you book this lesson for $90 right now? If not, what's the price you'd book it at?" Capture a number, not a vibe.
2. (To learners.) "Would you give the platform consent to keep this recording so it can train an AI assist for your future lessons?" — measure consent rate as a leading indicator of the moat.
3. (To masters, in Japanese.) "If we paid you ¥10,000–15,000 per 60-min lesson, with you keeping 70%, would you take 5 sessions/month from foreign learners over voice + video?" Capture a Y/N + a number.
4. (To masters.) "What part of this translation made you wince?" — surface the craft-jargon failures we'd need a glossary to fix.
5. (To club leaders.) "Would you pin the booking link in your club's Discord / mailing list, no commission?" — test whether organic distribution exists.

**Pass criteria:** ≥6 of 12 conversations end with a numeric WTP at or above $80, AND ≥3 Japan-resident masters verbally agree to a 5-lesson trial at 70% take, AND the screencast generates ≥1 inbound from a craft enthusiast not in Vincent's network within 14 days of public posting.

**Kill criteria:** <2 of 5 learners say they'd pay any price; OR ≥3 masters refuse the recording-consent ask outright; OR the live translation makes a wrong cut (master says "leave it," learner cuts) in the demo lesson and a second take cannot recover. Any of these breaks the load-bearing assumption.

**Vincent's effort:** ~50 hours total — 25 build + 5 in-lesson + 20 conversations and synthesis. Output: the public screencast, the booking page, and a memo with quoted answers + a go / pivot / kill recommendation. The same artifact serves as the seed of the supply-side demo reel for masters in vertical 2 if Tegaki goes.

## What we don't know yet

- Whether Meta Ray-Ban Display's first-person camera resolution at 30–40 cm hand-distance is actually high enough to resolve which-wire-on-which-branch detail under typical home lighting. Needs a sit-down demo before locking the device list.
- Whether iemoto and guild structures around named bonsai lineages will tolerate consent-to-record at all, or whether the first 30 masters need to come exclusively from outside-the-iemoto pools (Mirai-network expats, Western-trained Japan-residents).
- Where exactly the boundary lives between "consent-to-record so we can train AI" and the consumer-trust collapse the [Meta–Sama Kenya annotator dispute](https://www.bbc.com/news/articles/c5y7yvgy0w6o) just demonstrated. The answer probably lives in master-side data ownership and revenue-share on AI-derived products — needs a legal pass before scaling.
- Whether vertical 2 should be sushi (highest WTP, fuzziest outcome label, food-safety risk on translation latency) or kintsugi (cleaner outcome, allergen liability), or whether the right vertical 2 is something the data from vertical 1 surfaces unexpectedly.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Banto — Voice-first generative interface that turns a Japanese ryokan's own service standards into a per-shift operating system for the floor]]
- [[Atelier — Per-patient cognitive rehab apps generated for smart glasses from the patient's own home]]
- [[Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses]]
- [[Mensho — Multilingual cultural-rubric eval suite voice-AI vendors plug into CI to ship Japanese, French, and code-switching deployments without quality regressions]]
