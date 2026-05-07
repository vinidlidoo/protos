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

**Elevator pitch:** A two-sided marketplace where anyone, anywhere can put on smart glasses and learn a hands-on physical-world skill from a guide who watches your hands in real time, corrects you as you work, and earns from their own kitchen, studio, or workshop. Learners pay per session, guides earn globally, every session is recorded with consent, and by 2030 we displace YouTube tutorials (the video can't see what's in front of you) and the in-person workshop (expensive, rare, geography-gated) as the default place humans go to learn anything they do with their hands.

**How it works:** A learner in San Francisco books a session with a sushi guide in Osaka. The learner puts on smart glasses (Meta Ray-Ban Display or equivalent) and watches their own hands through the lens while the guide's hands float beside them in picture-in-picture. The guide watches the learner's first-person feed and talks them through it as they work, with English ↔ Japanese live translation with captions both ways. The guide corrects in real time: "rotate the blade five degrees, drop your shoulder." The learner can rewind the last 30 seconds of the guide's hands and voice on demand, replaying any correction until it sinks in. With consent, every session is recorded: first-person learner-hand video, guide audio corrections, and outcome rating join our corpus of reference data. We launch with a four-activity Japan-sourced basket (sushi knife-skills, pottery, woodworking joinery, gardening) for global consumer learners; expand supply and verticals across general hobby, skilled trades, and professional services in Phase 2; and in Phase 3 corpus-trained AI guides deliver a similar experience at a fraction of the cost.
## What's the problem?

Hands-on knowledge, anything humans do with bodies and tools, is the worst-documented category on the internet. AI is already a competent tutor for text-knowable subjects; it cannot tell you why your knife angle is wrong, because no one has shown it the million first-person videos of beginner hands being corrected that would teach it.

Today, a hobbyist who wants to learn sushi knife-skills, joinery, or thrown pottery has three real options: a YouTube video that can't see what they're doing wrong, a $4,000 trip to a Tokyo workshop, or a local instructor for the handful of skills that happen to have one nearby. The same scarcity bottlenecks every skilled trade: a new electrician apprentice learns by riding shotgun with one journeyman, a rural surgical resident sees one specialist's technique. The cost of "watching the right hands" makes whole crafts extinction-prone in the cultures where they were born.

## Why now?

*(as of May 2026)*

- **Smart glasses hit consumer scale in 2025, including the first display-equipped variant.** Meta + EssilorLuxottica sold 7M+ AI glasses in 2025, more than triple the prior two years combined *(Feb 2026)*; the category grew 139% YoY in H2 2025 with Meta at 82% share *(H2 2025)* ([CNBC](https://www.cnbc.com/2026/02/11/ray-ban-maker-essilorluxottica-triples-sales-of-meta-ai-glasses.html), [Display Daily](https://displaydaily.com/smart-glasses-shipments-doubled-in-second-half-of-2025-with-meta-commanding-82-of-the-market/)). The $799 Meta Ray-Ban Display launched September 2025 *(Sept 2025)* with US demand so heavy that international rollout was paused into 2026 *(Jan 2026)* ([CNBC](https://www.cnbc.com/2026/01/06/meta-ray-ban-display-ai-glasses-pause.html)); production is reportedly being doubled to 20M+ units in 2026 *(Bloomberg via CNBC, Jan 2026)* ([CNBC](https://www.cnbc.com/2026/02/11/ray-ban-maker-essilorluxottica-triples-sales-of-meta-ai-glasses.html)). A learner can now see the guide's hand picture-in-picture in their own lens.
- **The hardware became buildable for outside teams.** Snap's consumer "Specs" launch later in 2026 alongside a multi-year Qualcomm Snapdragon partnership *(Apr 2026)* ([Snap Investor](https://investor.snap.com/news/news-details/2025/Snap-to-Launch-New-Lightweight-Immersive-Specs-in-2026/default.aspx), [Road to VR](https://www.roadtovr.com/snap-qualcomm-partnership-specs-2026-ar-glasses/)). The Spectacles 5 dev kit and Snap OS 2.0 already expose documented camera, ASR (40+ languages), and WebXR APIs to third parties, with OpenAI and Gemini integrations via Snap's Remote Service Gateway *(Sept 2025)* ([Lowpass](https://www.lowpass.cc/p/snap-spectacles-webxr-native-apps)). Independent teams can experiment on smart glasses today, with consumer-grade hardware shipping by end of year.
- **Live translation crossed the practical bar.** Standalone AR translation glasses now ship with sub-500ms latency across 100+ languages *(CES, Jan 2026)* ([PR Newswire — LLVISION](https://www2.prnewswire.com/news-releases/llvision-introduces-leion-hey2-the-worlds-first-professional-ar-translation-glasses-launching-in-the-united-states-at-ces-2026-302654009.html)), and consumer-glasses live caption/translation tested at "nearly zero latency" in independent hands-on at the Meta Ray-Ban Display launch *(Sept 2025)* ([The Verge](https://theverge.com/tech/779566/meta-ray-ban-display-hands-on-smart-glasses-price-battery-specs)). Craft jargon and dialect remain hard, but mainline lesson speech is now in scope.
- **The remote-assist mechanic is proven at scale.** TeamViewer Frontline cuts new-hire onboarding 50–70% at DHL Supply Chain *(May 2026)* ([TeamViewer](https://teamviewer.com/en-us/products/frontline/platform)); Help Lightning has run 43M+ enterprise help sessions across 80+ countries *(May 2026)* ([Help Lightning](https://helplightning.com/solutions/)). "Expert sees what the worker sees, guides their hands" is a known, working pattern.

## Who else is doing this?

- **Industrial AR remote-assist (the closest mechanical analogue, sealed in B2B).** Main player: **[TeamViewer Frontline](https://teamviewer.com/en-us/products/frontline/platform)**. Others: [Help Lightning](https://helplightning.com/solutions/), [Augmentir](https://www.augmentir.com/product/industrial-collaboration), TeamViewer Frontline Assist. They sell into manufacturing / logistics / field-service buyers: enterprise contracts, IT-led procurement, certified-glasses lock-in to Vuzix / RealWear. The architecture works in production. The buyer, price point, and brand are all wrong for consumer or prosumer instruction.
- **Subscription craft-education libraries (closest to our supply quality in phase 1).** Main player: **[Bonsai Mirai Live](https://live.bonsaimirai.com/pricing)** ($9.99–$29.99/month). One-to-many recorded video, a single discipline, no live two-way feedback on the learner's own hands. Premium content, but it's a magazine, not a tutor.
- **Online live-tutoring marketplaces (closest to our marketplace shape in phase 1).** Main players: **[italki](https://www.italki.com/en/teachers/japanese)** (1,159 Japanese tutors at trial-price points spanning $5–$30, language-focused), [Preply](https://preply.com), [Cafetalk](https://cafetalk.com); [Outschool](https://outschool.com) for K-12 small-group classes. All built on a camera-on-the-teacher architecture, where the teacher's face or screen is the right thing to see. Hands-on skills require the camera on the *learner's* hands instead, so migrating them to glasses-first is a rebuild, not a feature.
- **Recorded-course platforms.** Main players: **[MasterClass](https://www.masterclass.com/sessions)** (annual subscription starting at £10/month billed annually, 200+ instructors), [Skillshare](https://www.skillshare.com/pricing) ($167.88/year, 11M+ creative members, 9,000+ teachers), [Udemy](https://udemy.com), [Coursera](https://coursera.org). One-to-many recorded video at scale. MasterClass has the brand and stars; Skillshare has the creator long tail. Their economics depend on infinite reuse of pre-recorded content; a live two-sided marketplace is a different business. Different unit economics, different supply chain, different product.

**Where the opening is:** every category above is shaped wrong for hands-on instruction. Industrial AR has the mechanic but the wrong buyer; craft libraries are one-way video; lesson marketplaces are camera-on-the-teacher; creator-led platforms are recorded broadcasts. Nobody is building a two-sided marketplace where the camera is on the *learner's* hands and the guide is remote, because the device that makes that ergonomic at the consumer level is just beginning to ship.

## Why us?

- **Japan supply + global demand fluency.** EN/FR/JA fluent, 10 years in Japan and 8 in the US; can cold-start shokunin supply in Tokyo / Kyoto / Osaka *and* close consumer demand in NA / EU.
- **Two-sided marketplace operator.** 5 years at Amazon Fashion across chief of staff, category management, and product management; inside view of one of the largest e-commerce verticals running on this mechanic.
- **AI-evaluation lead.** 2 years leading AI evals at Amazon, the expertise to understand the data needed from recorded sessions to orchestrate and fine-tune models that assist learners in their journey.
- **Ships solo with coding agents.** CS/AI depth, comfortable building end-to-end — the 2-week knife-skills demo gets to a working artifact without waiting on a hire.
## Who is the customer?

- **Learner:** the hobbyist. The home cook who follows half a dozen Japanese sushi YouTubers; the woodworker building a tansu in their garage; the gardener who reads English bonsai forums but has never had a guide cut alongside them.
	- **Profile:** 35–55, household income $100K+, in NA / EU / AU / SG, has spent ≥$500 on craft hobby supplies in the last year.
	- **Economics:** direct-to-consumer, no procurement loop. First-purchase ACV $80–$200 (one to three sessions). Repeat-buyer ACV $400–$1,200/year.
	- **ICP:** (a) has tried 3+ YouTube tutorials in the target craft and felt the camera was in the wrong place; (b) has never been able to find a local guide; (c) will pay ≥$80 for a 60-minute lesson; (d) owns smart-glasses-class hardware, or willing to use a Ray-Ban Meta + phone-on-the-bench fallback during launch.
- **Guide:** an independent shokunin running an atelier of 1–5 people, supplementing in-shop teaching with international students.
	- **Profile:** craftsman in cuisine, ceramics, joinery, or gardening. Already does some international teaching (Zoom, occasional fly-ins, written exchanges), rate-limited by travel and by how many students they can host in person.
	- **Economics:** ¥10,000–¥15,000/hour ($65–$100) net at our 20% take rate. Five recorded sessions per week is roughly $1,500–$2,500/month of incremental income with no travel. Online sessions also act as top-of-funnel for in-person visits: learners who connect with a guide remotely are more likely to fly out to study with them in person, adding high-margin in-shop bookings on top.
	- **ICP:** (a) speaks enough English to be guided by translation, or has a spouse / student / apprentice who does; (b) currently does some international teaching but is rate-limited by travel; (c) comfortable being recorded on a per-session, per-guide consent basis (not guild-level).
- **Anti-customer:** 
	- **Consent:** [Iemoto](https://en.wikipedia.org/wiki/Iemoto)-gated cultural arts (tea ceremony, ikebana, classical shodō), where consent to record is a guild-level conversation, not a per-guide one. We may sell here later; we will not lead with it.
	- **Liability:** regulated touch (medical, manual therapy, bodywork-class disciplines). Phase 2 territory, not launch.

## Where do we enter?

We'll launch with a basket of four Japan-sourced activities taught by independent Shokunin (Japanese craft masters): 1) sushi knife-skills, 2) pottery wheel, 3) kumiko joinery, and 4) Japanese gardening / pruning:

- **Sushi Knives:** "your knife technique, reviewed" ($120). Guide watches blade angle on three cuts, corrects in real time. *(Tokyo in-person classes run $53–$130: [Tokyo Sushi School](https://www.tokyosushischool.com/), [NOBU Sushi Making](https://www.tokyosushimaking.com/).)*
- **Pottery Wheel:** "centring + first pull" ($90). Guide watches the learner's hands at the wheel, corrects rotation and finger pressure live. *(Tokyo group classes start at ~$37; true 1:1 sessions run ~$247: [ActivityJapan](https://en.activityjapan.com/feature/tokyo-ceramics-plan/), [Uzumako Ceramic Art School](https://www.uzumakotougei.com/private-class/).)*
- **Joinery (kumiko):** "your first kumiko-pattern lap joint" ($180). Guide walks layout, marking, and one chiselled joint, watching tool angle on each cut. *(Tokyo private kumiko experiences run $280; Toyama's advanced course $100: [Deeper Japan](https://www.deeperjapan.com/tokyo/p/edo-kumiko-woodcrafting), [Kumikoza Toyama](https://www.toyamashi-kankoukyoukai.jp/en/experience/kumikoza/).)*
- **Gardening / pruning (bonsai-adjacent):** "what would you cut on this tree" ($80), learner walks the guide through their garden via first-person camera. Guide flags structural issues and proposes cuts. *(Tokyo bonsai workshops run $74–$128: [Japan Experience](https://www.japan-experience.com/activities/tokyo/bonsai-workshop-in-the-heart-of-tokyo), [Shunkaen Bonsai Museum](https://veronikasadventure.com/tokyo-bonsai-making-experience-with-bonsai-master/).)*

**Materials.** Each SKU's detail page lists what works for the session (knife type, clay grade, chisel sizes), with specific buy-options surfaced on Amazon for learners in NA / EU / UK / JP / AU. Learners outside those locales get the spec list and source locally. No inventory, no kit fulfillment, no shipping risk; affiliate revenue is upside, customer convenience is the point. Open question: whether Amazon catalogs in each locale carry Japanese-grade joinery and knife specs at acceptable quality.

The four are picked for **signal-shape diversity**: blade-on-food, wheel-mounted craft, tool-on-wood, and outdoor spatial reasoning. Recent embodied-AI work finds that scene, object, and demonstrator diversity drives generalization more than corpus size alone ([EgoVerse, arXiv 2604.07607](https://arxiv.org/abs/2604.07607)), so even a small Phase-1 corpus already spans four modalities. All four are also **non-iemoto**, sitting outside the guild-headmaster system that gates tea ceremony, ikebana, classical calligraphy, kōdō, traditional dance, traditional music, and martial arts. Consent-to-record is a per-guide conversation, not a guild-level one. Finally, **demand is large and English-speaking**. Reddit communities alone aggregate millions: r/Pottery 263k, r/Bonsai 360k, r/sushi 583k, r/woodworking 6.1M. Flagship English-language YouTube supply matches: Hiroyuki Terada 2.1M (sushi), Florian Gadsby 1.8M (pottery), ISHITANI Furniture 605k (Japanese joinery), and Bonsai Mirai serving "thousands of enthusiasts across 52 countries" with 600+ videos.
## What makes it defensible?

The moat shifts over time:

- **Two-sided network effects (Phase 1–2 steady-state).** More guides, more learners, more guides. Once supply density per activity passes ~100, the marketplace becomes the *default destination* for that activity, and both sides face real switching costs: guides earn from the inbound demand pool, learners get the broadest discovery and reviews. italki long-tail languages show the threshold is real at single-niche scale ([Greek 162](https://www.italki.com/en/teachers/greek), [Vietnamese 77](https://www.italki.com/en/teachers/vietnamese), [Czech 72](https://www.italki.com/en/teachers/czech)). Preply shows the flywheel compounds: 100K tutors / 90 languages, $1.2B unicorn, EBITDA-profitable in Jan 2026 ([TechCrunch](https://techcrunch.com/2026/01/21/language-learning-marketplace-preplys-unicorn-status-embodies-ukrainian-resilience/)).
- **Recorded corpus (Phase 3).** Every consented session captures the (first-person hand video, guide correction, outcome rating) triplet, the modality that makes the corpus trainable for embodied AI guides; volume alone doesn't substitute. Ego-Exo4D, the state-of-the-art open dataset of paired first-person + expert-commentary skilled-activity video, is ~1,400 hours and took a 15-institution consortium two years to build ([Ego-Exo4D](https://docs.ego-exo4d-data.org/)); a 3-year Waza ramp of 100k–300k 60-min sessions yields 70×–215× more, in the exact annotation modality researchers had to synthetically construct. 
- **Category brand (by 2030).** The default consumer answer to "I want to learn anything I do with my hands," the way YouTube became default for "I want to watch X." A late-mover OEM or content platform then faces a recognition gap on top of the corpus and network-effects moats. The elevator's 2030 ambition is itself the third moat.

**Honest two-stage caveat.** This is a two-stage company. If world models for embodied tasks stay immature through 2030, we are still a $1–3B marketplace. If they mature, we own the only training corpus that can produce AI guides in this category, and the prize is $50B+.

## How it could make money?

The unit-economics story shifts by phase. **Phase 1** rides a Japan-supply / international-demand asymmetry as the launch wedge: Tokyo guide labour at ¥10,000–¥15,000/hour ($65–$100) sits well above in-shop teaching rates yet comfortably below the international learner's $80–$200/session WTP. **Phase 2** generalizes the same shape wherever local expert hourly is below international learner WTP (Vietnamese joinery, Indian surgical mentorship, Eastern-European trades, French patisserie) once the marketplace recruits beyond Japan. **Phase 3** flips the model: AI guides drive marginal cost toward zero, and the asset shifts from per-session take to the corpus itself. We monetize across all three regimes in four stacked layers.

- **Layer 1 — Marketplace take rate (Phase 1 primary).** 20% on $80–$200 sessions: ~$16–$40 gross per session, roughly $10–$30 contribution after Stripe + AV infrastructure. Comp: [italki 15–21%](https://support.italki.com/hc/en-us/articles/206352068-How-does-italki-charge-a-commission). Defensible at the top of that band wherever local-expert hourly sits below international-learner WTP. Japan at ¥10K–¥15K/hr is the launch case, but the same arithmetic carries any expert market outside North America.
- **Layer 2 — Learner subscription (Phase 2, stacks on Layer 1).** $19–$39/month for: a 24/7 AI-assist that answers craft questions between live sessions; access to the recorded-session library across all guides who consented; 10% off live bookings. Comp: [Bonsai Mirai $9.99–$29.99/mo](https://live.bonsaimirai.com/pricing) for one-way video on a single discipline; [MasterClass from £10/mo](https://www.masterclass.com/sessions) for passive video. We bracket higher because the AI-assist is the product, not a bolt-on.
- **Layer 3a — AI-guide SaaS (Phase 3 consumer).** $30–$200/month for AI guides trained on the corpus, delivering a similar live-correction experience at a fraction of human cost. Comp bracket: [Khanmigo ~$44/yr](https://www.khanmigo.ai/), [Duolingo Max $30/month](https://www.duolingo.com/max), Synthesis Tutor — the AI-tutoring SaaS bracket, not the recorded-content one.
- **Layer 3b — Corpus licensing (Phase 3 B2B).** $100k–100M/year to AI labs and embodied-AI vendors. No clean public comp because nobody licenses embodied-task corpora yet; closest analogues are Scale AI / Surge AI proprietary-set pricing and genomics-data licensing precedents. Soft on this tier until the corpus is sized.

## What would pressure the thesis?

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
5. **Assumption: the marketplace moat survives an Apple, Meta or Google smart-glasses-native first-party "tutoring" feature.**
   - **What would pressure it:** Meta launches a "Find an Expert" surface natively in Ray-Ban Display, where any verified expert can be discovered without an app install.
   - **Lever:** lean hard on the corpus and the Phase 3 AI-guide product as the actual moat. The marketplace surface is commoditisable; the corpus is not. This is the Phase 3 transition we've already named.
6. **Assumption: marketplace trust survives consumer awareness of deepfake AI guides.**
   - **What would pressure it:** real-time generative video makes a fake "Osaka shokunin" indistinguishable from a real one on a learner's lens before we have reputation density, OR a wave of fake-guide scams in adjacent live-tutor marketplaces poisons buyer trust.
   - **Lever:** verified-human-on-both-sides becomes a launch-day feature. Nearly 18M people have verified at a World ID Orb globally ([World](https://world.org/blog/announcements/world-id-full-stack-proof-of-human)); the network is rolling out through 3,000 Japanese locations via the MEDIROM partnership ([Globe Newswire](https://www.globenewswire.com/news-release/2026/01/23/3225091/0/en/MEDIROM-Forms-New-Special-Mission-Team-to-Drive-World-ID-Adoption-Across-3-000-Locations-Through-Partnership-with-Tools-for-Humanity.html)). The coverage path maps directly onto our supply geography.
7. **Assumption: the window before incumbents can match this architecture is roughly 18 months.**
   - **What would pressure it:** consumer smart-glasses adoption stalls past 2027 and the window stretches to 36+ months (urgency premium evaporates), OR an OEM ships a native "Find an Expert" surface within 6–12 months (window collapses; see Risk #5).
   - **Lever:** plan capital around the tight assumption (2-year experiment-to-Series-A on a 5–10 person team) but build corpus quality from day one, so a longer window only deepens the moat.

## 2-week experiment

**Load-bearing assumption to test:** when a learner has a remote Japanese guide watching their hands in real time and correcting them, does it feel meaningfully better than a YouTube tutorial, enough to pay $80–$200 and book again?

**Artifact to build (week 1):** a working single-lesson demo for **knife-skills** (lowest hardware overhead, highest demand-side legibility, fastest to produce). Vincent solo + coding agents builds:
- A web app + simple iPhone webview that brokers a two-way video session between a Japanese guide and a learner. **Phone propped on the cutting board** is the learner's camera; the guide watches on laptop. Live translation via Whisper streaming + GPT-4o realtime + ElevenLabs TTS in both directions.
- Record-on-consent at start, end-of-session 1–5 rating.
- One separate run with **Snap Spectacles** (Vincent as the learner in Montreal) to gut-check the smart-glasses form factor and produce a short screencast asset. Phone-on-stand is the experiment's hardware; the Spectacles run is qualitative.

5 working days, doable solo with coding agents.

**Conversations (week 2):** 5 paid lessons ($120 each) with real international learners sourced from r/sushi / r/Japanesefood / a Japan-sushi-Twitter post. Each session opens with the artifact, not a deck. Vincent observes every session as silent operator. Time-zone shift is a challenge (JP↔NA, 13–16h); the booking UI surfaces guide local time and prefers JP-evening / NA-morning slots.

**Two questions, asked at session end** (verbatim, recorded):
1. What did this session do that the last YouTube knife-skills video you watched could not?
2. Would you book another at $120? At $180?

Pricing-ladder follow-up + 4-session prepay offer ($400) go via email within 48h. Keeps the live debrief tight.

**Pass criteria** (need 2 of 3):
- ≥4/5 learners name a specific concrete dimension where the session beat YouTube (not "it was nice").
- ≥3/5 prepay the 4-session pack when offered by email.
- The guide's qualitative read: enjoyed it, wants to do more.

**Fail criteria:** ≤2/5 would book again, OR translation breaks the lesson on >2 of 5 sessions in a way the guide can't work around.

**Vincent's effort:** ~50 hours week 1 (build), ~20 hours week 2 (5 sessions + scheduling + write-up). Output: hosted demo + Spectacles screencast + memo with quoted answers + go / pivot / kill recommendation.

## What we don't know yet?

- **Smart-glasses front-camera signal at hand distance.** Resolution and framerate at 20–40cm under typical kitchen, workshop, and outdoor lighting: does it preserve the signal a guide needs to correct knife angle and tool grip? 
- **Cross-jurisdiction recording-consent law.** A Japanese guide recording a US learner's hands in their US kitchen: whose consent statute governs, and how does the matrix shift for EU and AU learners? Phase 2 expansion multiplies the pairs.
- **Supply norms inside and outside Japan.** Within Japan, do shokunin in joinery / pottery / cuisine carry unwritten apprentice-only norms against teaching foreigners that we'd be violating? Outside Japan, does the informal-shokunin layer even have an analog, or is Phase 2 supply (Vietnamese trades, Indian surgical mentorship, Eastern-European craft, French patisserie) closer to guild-gated than informal?
- **First-session price elasticity.** $80 vs $120 vs $180; the experiment only tests $120.