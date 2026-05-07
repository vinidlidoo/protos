---
id: proto-waza
aliases:
  - Waza
tags:
  - proto
type: proto
status: shortlisted
created: 2026-05-07
origin: ad-hoc seeded run v2 — locked thesis, brief-driven
proto_generator:
  seed: 477611875
  writer_index: 1
  repo_sha: 1d05c7b8a4022c970e37d7886e1ba37e5ad12679
  generated_at: 2026-05-07T00:22:36Z
  mode: ad-hoc-seeded
---
# Waza — Live, hands-on tutoring through smart glasses

## What is it?

**Elevator pitch:** A two-sided marketplace where anyone, anywhere can put on smart glasses and learn a hands-on physical-world skill from a guide who watches your hands in real time, corrects you as you work, and earns from their own kitchen, studio, or workshop. Learners pay per session, guides earn globally, every session is recorded with consent — and by 2030 we displace YouTube tutorials (the video can't see what's in front of you) and the in-person workshop (expensive, rare, geography-gated) as the default place humans go to learn anything they do with their hands.

**How it works:** A learner in San Francisco books a session with a sushi guide in Osaka. The learner puts on smart glasses (Meta Ray-Ban Display or equivalent) and watches their own hands through the lens while the guide's hands float beside them in picture-in-picture. The guide watches the learner's first-person feed and talks them through it as they work, with English ↔ Japanese live translation with captions both ways. The guide corrects in real time: "rotate the blade five degrees, drop your shoulder." The learner can rewind the last 30 seconds of the guide's hands and voice on demand, replaying any correction until it sinks in. With consent, every session is recorded: first-person learner-hand video, guide audio corrections, and outcome rating join our corpus of reference data. We launch with a four-activity Japan-sourced basket (sushi knife-skills, pottery, woodworking joinery, gardening) for global consumer learners; expand supply and verticals across general hobby, skilled trades, and professional services in Phase 2; and in Phase 3 corpus-trained AI guides deliver a similar experience at a fraction of the cost.
## What's the problem?

Hands-on knowledge, anything humans do with bodies and tools, is the worst-documented category on the internet. AI is already a competent tutor for text-knowable subjects; it cannot tell you why your knife angle is wrong, because no one has shown it the million first-person videos of beginner hands being corrected that would teach it.

Today, a hobbyist who wants to learn sushi knife-skills, joinery, or thrown pottery has three real options: a YouTube video that can't see what they're doing wrong, a $4,000 trip to a Tokyo workshop, or a local instructor for the handful of skills that happen to have one nearby. The same scarcity bottlenecks every skilled trade: a new electrician apprentice learns by riding shotgun with one journeyman, a rural surgical resident sees one specialist's technique. The cost of "watching the right hands" makes whole crafts extinction-prone in the cultures where they were born.

## Why now?

*(as of May 2026)*

- **Smart glasses crossed consumer adoption in 2025.** Meta + EssilorLuxottica sold over 7 million AI glasses in 2025 alone, more than triple the prior two years combined ([CNBC](https://www.cnbc.com/2026/02/11/ray-ban-maker-essilorluxottica-triples-sales-of-meta-ai-glasses.html)), and the category grew 139% year-on-year in H2 2025 with Meta at 82% share ([Display Daily](https://displaydaily.com/smart-glasses-shipments-doubled-in-second-half-of-2025-with-meta-commanding-82-of-the-market/)). Production guidance is now 20M+ units for 2026 ([CNBC](https://www.cnbc.com/2026/02/11/ray-ban-maker-essilorluxottica-triples-sales-of-meta-ai-glasses.html)).
- **The first display-equipped consumer glasses shipped at scale.** The $799 Meta Ray-Ban Display launched in September 2025 with such overwhelming US demand that international rollout was paused into 2026 ([CNBC](https://www.cnbc.com/2026/01/06/meta-ray-ban-display-ai-glasses-pause.html)). A learner can now see the guide's hand picture-in-picture in their own lens.
- **Live translation crossed the practical bar.** Standalone AR translation glasses now ship with sub-500ms latency across 100+ languages ([PR Newswire — LLVISION CES 2026](https://www2.prnewswire.com/news-releases/llvision-introduces-leion-hey2-the-worlds-first-professional-ar-translation-glasses-launching-in-the-united-states-at-ces-2026-302654009.html)), and Meta AI translation is a flagship Ray-Ban feature ([Meta Store](https://www.meta.com/ai-glasses/meta-ray-ban-display/)). Craft jargon and dialect remain hard, but mainline lesson speech is now in scope.
- **Industrial AR remote-assist proved the underlying mechanic at scale.** TeamViewer Frontline cuts new-hire onboarding time ~50% at DHL Supply Chain, with 1,500 employees using it daily across 25 US sites ([TeamViewer](https://teamviewer.com/en-us/products/frontline/platform)); Help Lightning has run 38M+ enterprise help sessions across 80+ countries ([Help Lightning](https://helplightning.com/solutions/)). "Expert sees what the worker sees, guides their hands" is a known, working pattern — just sealed inside enterprise field-service contracts.
- **Proof-of-humanity infrastructure is rolling out in our launch geography.** Nearly 18M people have verified their humanness at a World ID Orb globally ([World](https://world.org/blog/announcements/world-id-full-stack-proof-of-human)), and the network is deploying through 3,000 Japanese locations via the MEDIROM partnership ([Globe Newswire](https://www.globenewswire.com/news-release/2026/01/23/3225091/0/en/MEDIROM-Forms-New-Special-Mission-Team-to-Drive-World-ID-Adoption-Across-3-000-Locations-Through-Partnership-with-Tools-for-Humanity.html)). For a marketplace where buyers worry about deepfake "guides," verified-human-on-both-sides becomes a feature rather than a moat.

## Who else is doing this

- **Industrial AR remote-assist (the closest mechanical analogue).** Main player: **[TeamViewer Frontline](https://teamviewer.com/en-us/products/frontline/platform)**. Others: [Help Lightning](https://helplightning.com/solutions/), [Augmentir](https://www.augmentir.com/product/industrial-collaboration), TeamViewer Frontline Assist. They sell into manufacturing / logistics / field-service buyers (enterprise contracts, IT-led procurement, certified-glasses lock-in to Vuzix / RealWear). They have proven the mechanic but cannot pivot to consumer/prosumer instruction — different buyer, different distribution, different price point, no consumer brand.
- **Subscription craft-education libraries (closest to our supply quality).** Main player: **[Bonsai Mirai Live](https://live.bonsaimirai.com/pricing)** ($9.99–$29.99/month across Basic / Standard / Pro tiers). One-to-many recorded video, a single discipline, no live two-way feedback on the learner's own hands. Premium content, but it's a magazine, not a tutor.
- **Online lesson marketplaces (closest to our marketplace shape).** Main players: **[italki](https://www.italki.com/en/teachers/japanese)** (1,159 Japanese tutors at trial-price points spanning $5–$30), [Preply](https://preply.com), [Cafetalk](https://cafetalk.com). All optimized for language tutoring over a webcam, where the camera being pointed at the teacher's face is correct. They cannot teach hands-on skills because the camera-on-the-guide architecture loses the learner's hands. Migrating them to glasses-first is a rebuild, not a feature.
- **Live-class and creator-led platforms.** Main players: **[MasterClass](https://www.masterclass.com/sessions)** (annual subscription starting at £10/month billed annually, 200+ instructors), [Skillshare](https://www.skillshare.com/pricing) ($167.88/year, 11M+ creative members, 9,000+ teachers), [Outschool](https://outschool.com), [Udemy](https://udemy.com), [Coursera](https://coursera.org). One-to-many recorded video at scale. MasterClass has the brand and stars; Skillshare has the creator long tail; none have a hands-on-feedback architecture or any reason to acquire one — they are content companies, not marketplaces.

**Where the opening is:** every category above is shaped wrong for hands-on instruction. Industrial AR has the mechanic but the wrong buyer; craft libraries are one-way video; lesson marketplaces are camera-on-the-teacher; creator-led platforms are recorded broadcasts. Nobody is building a two-sided marketplace where the camera is on the *learner's* hands and the guide is remote — because the device that makes that ergonomic only just shipped to consumers in 2025. We are an 18-month window into a hardware platform shift; the incumbents will see the opportunity but cannot pivot their go-to-market without cannibalising their existing book.

## Why us

- **Vincent's combined Japan-supply / global-demand fluency is the wedge's bottleneck-shaped advantage.** 10 years living in Japan plus EN/FR/JA fluency plus direct Amazon two-sided-marketplace operating experience (5 years in Fashion: chief of staff, category management, product management) is a one-person fit for the supply-side cold start in Tokyo / Kyoto / Osaka and the demand-side go-to-market in NA + EU. The Phase 1 task is "find 50 informal-supply-pool guides across four crafts and get the first 1,000 international learners to book"; this attribute set lines up with that task more cleanly than for any of the listed comparables.
- **Direct AI-evaluation experience pre-positions us for the Phase 3 corpus → AI-guide leg.** 2 years at Amazon leading model evaluations including specialised ASR/audio work — the exact discipline needed to know whether the recorded corpus actually preserves the signal the AI guide will need.

## Customer & buyer

- **Customer:** the international hobbyist learner — the home cook who follows half a dozen Japanese sushi YouTubers; the woodworker building a tansu in their garage; the gardener who reads English bonsai forums but has never been pruned-by a guide. Median profile: 35–55, household income $100K+, in NA / EU / AU / SG, has spent ≥$500 on craft hobby supplies in the last year, has bought a smart-glasses-class device or is on the waitlist.
- **Buyer:** same person — direct-to-consumer, no procurement loop. Typical first-purchase ACV $80–$200 (one to three sessions), repeat-buyer ACV $400–$1,200/year.
- **Champion (supply side):** the guide themselves — typically a shokunin running an independent atelier of 1–5 people, supplementing in-shop teaching with international students who used to fly in once a year. We replace those flights with five recorded sessions per week.
- **ICP test:** consumer learner who (a) owns smart-glasses-class hardware, (b) has tried 3+ YouTube tutorials in the target craft and felt the camera was in the wrong place, (c) has never been able to find a local guide, (d) will pay ≥$80 for a 60-minute lesson. Guide who (a) speaks enough English (or has spouse/student who does — translation handles the rest), (b) currently does some international teaching but is rate-limited by travel, (c) has equity in being part of the corpus that trains future AI guides of their craft.
- **Anti-customer:** any iemoto-gated cultural art (tea ceremony, ikebana, classical shodō) where consent to record is a guild-level conversation rather than a per-guide conversation. We may sell into these later; we will not lead with them. Also any activity that requires regulated touch (medical procedures, bodywork) — Phase 3 territory, not launch.

## Wedge / where we could enter

We launch with **a basket of four Japan-sourced informal-supply activities — Shokunin: sushi knife-skills, pottery wheel, woodworking joinery, Japanese gardening / pruning.** The basket spans cuisine, wheel-mounted craft, tool-use craft, and outdoor spatial-reasoning craft, giving the recorded corpus signal-shape diversity from day one. All four pull from independent shokunin (not iemoto-gated), so consent-to-record is a per-guide conversation, and each has a recognizable global demand pull.

**First SKU per activity:**
- **Sushi knife-skills:** 60-min one-on-one "your knife technique, reviewed" — $120. Guide watches your blade angle on three cuts, corrects in real time.
- **Pottery wheel:** 75-min "centring + first pull" — $90.
- **Joinery:** 90-min "your first kumiko-pattern lap joint" — $180.
- **Gardening / pruning:** 60-min "what would you cut on this tree" — $80, walking the guide through your garden via first-person camera.

Phased path (Phase 1 launch basket, Phase 2 supply and vertical expansion across hobby + skilled trades + professional services, Phase 3 corpus-trained AI guides at a fraction of the cost) is described in How-it-works above and underwrites the defensibility section below.

## What makes it defensible

- **(a) Primary — the recorded-corpus data moat.** Every consented session adds first-person learner-hand video + guide audio corrections + outcome rating. After 3 years and 1M+ sessions, this is the only labelled dataset of "hands doing X badly, here's the correction, here's the outcome." YouTube can't capture it (camera on the wrong actor); industrial AR vendors have fragments behind enterprise NDAs.
- **(b) Secondary — two-sided marketplace network effects.** More guides → more learners → more guides. Standard, real once past 100 guides per activity, and shielded by Japan-supply expertise during cold-start.
- **(c) Year-3 endgame — category brand.** Default consumer answer to "I want to learn X hands-on," the way YouTube became default for "I want to watch X."

**Honest layer-N caveat (mandatory).** This is a two-stage company. **Today (Phase 1–2)** the product is a marketplace; the moat is network effects + brand + the corpus accumulating. **Tomorrow (Phase 3)** the product is an AI-guide company; the moat is the corpus itself plus the data-generation flywheel only this marketplace produces. Different buyers, different competitive sets, neither stage hidden. We are not papering over the transition with "we'll pivot" — Stage 1 is built to be a viable standalone marketplace AND the only economically rational way to acquire the Stage 3 substrate. If world models for embodied tasks stay immature through 2030, we are still a $1–3B marketplace; if they mature, we are the only candidate to be the $50B+ category-defining AI-guide company because we own the only training corpus.

## How it could make money

| Layer | Price range | Comparable |
| ----- | ----------- | ---------- |
| **Layer 1 — marketplace take rate (Phase 1 primary)** | 20% take on $80–$200 sessions | [italki commission schedule](https://support.italki.com/hc/en-us/articles/206352068-How-does-italki-charge-a-commission) runs 15%–21% depending on package size; we take in that band because we provide hardware-class infrastructure (recording, translation, glasses support) that italki does not. |
| **Layer 2 — learner membership (Phase 2 compounds)** | $19–$39/month | [Bonsai Mirai](https://live.bonsaimirai.com/pricing) ($9.99–$29.99/month) for one-way video; [MasterClass](https://www.masterclass.com/sessions) starting at £10/month billed annually. We bracket above MasterClass given AI-assist and live discounts in the bundle. |
| **Layer 3 (later) — AI-guide SaaS + corpus B2B (Phase 3)** | $30–$200/month consumer; $100K–$10M/year B2B licensing | Skillshare ($167.88/year, [Skillshare](https://www.skillshare.com/pricing)) for the consumer floor. B2B corpus licensing comparable bracket borrows from speech-data licensing (e.g., Common Voice / Defined.ai-class deals); soft on this tier until the corpus is sized. |

The Japan-supply / international-demand asymmetry is the unit-economics edge: Tokyo guide labour at ¥10,000–¥15,000/hour ($65–$100) is profitable for the guide and well below the international learner's WTP at $80–$200/session.

**Honest caveat.** Marketplace cold-start is the dominant business-model risk: 50 guides across 4 activities is a real bootstrapping ask, and if monthly session volume per guide falls below ~20, guides churn and the supply side collapses. Layer 1 is sufficient to fund Phase 2 only if the take-rate sticks at 20%; Stripe-class fee compression is plausible by 2028 and would shift the business toward subscription earlier than planned.

## What would pressure the thesis

1. **Assumption: smart glasses with picture-in-picture display reach 50M+ consumer units globally by end of 2027.**
   - **What would pressure it:** Meta production-scale guidance slips below 15M for 2026, OR international rollouts continue stalling beyond H1 2027 ([CNBC delay reporting](https://www.cnbc.com/2026/01/06/meta-ray-ban-display-ai-glasses-pause.html)), OR a regulatory backlash on always-on cameras kills consumer adoption in EU.
   - **Lever:** ship a phone-tripod fallback for the learner side (worse ergonomics, still functional) for the first 24 months; defer Phase 2 expansion until glasses TAM is real.
2. **Assumption: live translation at session-quality latency works for craft jargon, dialect, and honorifics, not just travel-phrases.**
   - **What would pressure it:** post-launch session-feedback shows >30% of cross-language sessions report "translation broke a key correction." LLVISION's sub-500ms claim is for "real-world use" but their training set is conference speech, not pottery dialect ([LLVISION CES 2026](https://www2.prnewswire.com/news-releases/llvision-introduces-leion-hey2-the-worlds-first-professional-ar-translation-glasses-launching-in-the-united-states-at-ces-2026-302654009.html)).
   - **Lever:** invest in a craft-vocabulary fine-tune on top of base MT — small specialised glossary per activity, guides review and ratify the glossary, prosody-aware audio scoring layer (the audio-acoustic moat pointer in the kit). This is plausibly where the deeper moat ends up living.
3. **Assumption: the recorded session captures enough signal to train Phase 3 AI guides.**
   - **What would pressure it:** first-person video at hand-distance in low-light kitchens / outdoor gardens turns out to be too low-resolution / too motion-blurred for fine-grained correction labels; or end-of-session outcome ratings are too noisy. The kit's "data-attribution chain" pointer specifically flags this.
   - **Lever:** dual-stream capture (glasses + a wide-angle desk camera the learner positions) for activities where hand-distance video is the bottleneck; explicit per-cut / per-pull rating UX rather than session-end-only.
4. **Assumption: supply-side cold start works — 50 informal-supply guides across 4 activities sign in 6 months.**
   - **What would pressure it:** guides refuse to record sessions citing IP / moral rights / iemoto-adjacent norms, OR the take rate is unattractive vs. their existing in-person teaching, OR Japanese guide generation skews older than smart-glasses comfort.
   - **Lever:** start with guides who already do international Zoom teaching (revealed-preference signal); offer a recording-revenue-share so guides get paid each time their corpus is licensed; pair every guide with a Japanese-fluent ops person who handles the glasses on their end.
5. **Assumption: the marketplace moat survives a Meta or Google smart-glasses-native first-party "tutoring" feature.**
   - **What would pressure it:** Meta launches a "Find an Expert" surface natively in Ray-Ban Display, where any verified expert can be discovered without an app install.
   - **Lever:** lean hard on the corpus and the Phase 3 AI-guide product as the actual moat — the marketplace surface is commoditisable, the corpus is not. This is the layer-N transition we've already named.

## 2-week experiment

**Load-bearing assumption to test:** when an international learner watches a remote Japanese guide watch their hands in real time and correct them, does the resulting learning experience feel meaningfully better than a YouTube tutorial — enough that the learner will pay $80–$200 and book again?

**Artifact to build (week 1):** a working **single-lesson demo** for one activity from the Shokunin basket. Pick **knife-skills** (lowest hardware overhead, highest demand-side legibility, fastest to produce). Vincent solo + coding agents builds:
- A web app + simple iPhone webview that brokers a two-way video session between a Japanese guide (Vincent's network — sushi shokunin or knife-craftsman, 1 person) and 5 learners.
- The learner uses Meta Ray-Ban Display (or Ray-Ban Meta + phone propped on the cutting board) for first-person hand video; the guide uses a phone or laptop. Live translation via Whisper streaming + GPT-4o realtime + ElevenLabs TTS in both directions.
- Record-on-consent at start, end-of-session 1–5 rating + free-text "did this beat YouTube?" prompt.
- Public 5-min screencast on X showing the full loop end-to-end with one real learner cutting.

5 working days, doable solo with coding agents.

**Conversations (week 2):** 5 paid lessons ($120 each) with real international learners sourced from r/sushi / r/Japanesefood / a Japan-sushi-Twitter post. Each session opens with the artifact (the guide is already in their lens), not a deck. Vincent observes every session as silent operator.

**Specific questions / asks** (asked at session end with the artifact still in front of them):
1. Compared to the last YouTube knife-skills video you watched, what did this session do that the video could not?
2. Would you book another session at $120? At $180? At $240?
3. What was the worst moment of friction (translation lag, video angle, glasses comfort, payment)?
4. Would you commit to 4 sessions over 8 weeks at $400 prepaid?
5. Which other Shokunin-basket activity would you want next — pottery, joinery, or gardening?

**Pass criteria:** ≥4/5 learners say the session beat YouTube on a specific concrete dimension (not just "it was nice") AND ≥3/5 prepay the 4-session pack AND the X screencast gets ≥1,000 likes / ≥3 inbound DMs from would-be guides or learners AND ≥1 guide from outside Vincent's direct network (cold-inbound from screencast) signs an LOI.

**Kill criteria:** ≤2/5 learners would book again AND no guide inbound from screencast AND/OR translation breaks the lesson on >2 of 5 sessions in a way the guide can't work around.

**Vincent's effort:** ~50 hours week 1 (build), ~20 hours week 2 (5 sessions × 90min + 5 hours of guide-side scheduling + ~10 hours of write-up). Output: hosted demo + screencast + memo with quoted answers + go / pivot / kill recommendation.

## What we don't know yet

- Smart-glasses front-camera resolution and framerate at 20–40cm hand distance under typical kitchen / workshop / outdoor lighting — does it actually preserve the signal a guide needs to correct knife angle / tool grip? No firsthand spec test yet.
- Cross-jurisdiction recording-consent law: a Japanese guide recording a US learner's hands in their own US kitchen — whose consent statute governs, and does it differ for EU learners?
- Iemoto-adjacent informal-supply norms: even within "informal supply," do shokunin in (e.g.) joinery have an unwritten apprentice-only norm against teaching foreign learners that we'd be violating?
- The actual price elasticity of $80 vs $120 vs $180 first-session pricing — the experiment tests $120 only.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Tegaki — Hands-free remote tutoring marketplace where Japanese masters teach physical-world skills over smart glasses to learners worldwide]] — the rejected v1 of this run, kept for record. Same wedge, narrower (Japan-bonsai-only) framing.
- [[Banto — Voice-first generative interface that turns a Japanese ryokan's own service standards into a per-shift operating system for the floor]] — sibling smart-glasses bet, different buyer (B2B Japan ryokan).
- [[Sterile — HIPAA-compliant clinical capture layer for consumer smart glasses]] — adjacent smart-glasses-as-capture bet in healthcare; informs Phase 3 medical-procedures vertical.
- [[Tessera — Fit-confidence API for agent-mediated apparel commerce trained on smart-glasses body capture]] — adjacent smart-glasses-as-capture bet; same hardware substrate, different vertical.
