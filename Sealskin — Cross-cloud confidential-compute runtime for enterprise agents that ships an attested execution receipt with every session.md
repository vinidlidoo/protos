---
id: proto-sealskin
aliases:
  - Sealskin
tags:
  - proto
type: proto
status: drafted
created: 2026-05-04
origin: ""
proto_generator:
  seed: 606433052
  writer: 1
  writers_total: 1
  repo_sha: 1d05c7b
  generated_at: 2026-05-04T21:48:53+00:00
---

# Sealskin — Cross-cloud confidential-compute runtime for enterprise agents that ships an attested execution receipt with every session

## What is it?

**Elevator pitch**: Sealskin is the runtime that lets a regulated enterprise's coding, ops, and analytics agents run against private source code, customer PII, and production credentials — by giving every agent session a hardware-attested confidential-compute sandbox and a signed receipt the buyer's auditors can verify offline. The platform team buys it because it unblocks the agents the business already wants to ship; the security team approves it because the receipts make the trust boundary cryptographic, not contractual.

**How it works**: The customer points a `sealskin run` command at any agent harness (Claude Agent SDK, OpenAI Agents SDK, LangGraph, Microsoft Agent Framework). Sealskin schedules the session into a confidential VM (AWS Nitro Enclave, Azure Confidential VM with TDX, or GCP Confidential VM with SEV-SNP — single API across all three), brokers the model call through an enclave-pinned outbound proxy, and emits a signed attestation document that binds together the enclave measurement, the harness commit hash, the model endpoint, the inputs hashed, and the tool calls made. The receipt verifies offline against the cloud's hardware root of trust and Sealskin's transparency log; the customer's compliance team can audit any session months later without re-running it.

## What's the problem?

Enterprises with private code, regulated data, or contractual confidentiality cannot let their agents touch the most valuable workloads, because every mainstream agent path leaks context to a vendor that retains it — Anthropic stores 30 days of Claude Code conversations and OpenAI is now under court order to preserve all output logs indefinitely ([IronCore writeup citing both retention policies](https://ironcorelabs.com/blog/2026/ai-coding-agents-drawing-the-line/)). Today these teams either ban agents on private repos outright (IronCore's published policy: "[Coding assistants are not allowed to process code bases that aren't open source](https://ironcorelabs.com/blog/2026/ai-coding-agents-drawing-the-line/)"), bolt the agent onto a single cloud's first-party runtime that doesn't emit verifiable execution proofs, or hand-roll a confidential-computing stack with [Anjuna or Fortanix](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) that wasn't designed for the agent loop. The result is the most valuable agent workloads — the ones touching the IP, the customers, and the production system — are the ones that don't ship.

## Why now (2026)

- **The hyperscalers just declared "every agent needs its own computer" — but neither Microsoft nor AWS ships a verifiable execution receipt.** Microsoft Foundry's hosted-agent service launched April 2026 with "every single agent session its own dedicated, isolated sandbox" and "production-proven hypervisor isolation" ([Microsoft Foundry blog](https://devblogs.microsoft.com/foundry/introducing-the-new-hosted-agents-in-foundry-agent-service-secure-scalable-compute-built-for-agents/)); AWS Bedrock AgentCore ships analogous "complete session isolation" ([AWS](https://aws.amazon.com/bedrock/agentcore/)). Both validate that enterprises will pay for agent-isolated compute. Neither emits a hardware attestation document the buyer can verify outside the cloud's own trust boundary — the gap Sealskin fills.
- **The hardware primitives finally cover all three clouds with cryptographic attestation built in.** AWS Nitro Enclaves "includes cryptographic attestation for your software, so that you can be sure that only authorized code is running" ([AWS](https://aws.amazon.com/ec2/nitro/nitro-enclaves/)); Google Cloud Confidential VM supports SEV-SNP and Intel TDX with "launch endorsements" signed by Google and verifiable against the hardware root of trust ([GCP docs](https://cloud.google.com/confidential-computing/confidential-vm/docs/attestation)). The substrate is mature enough that a cross-cloud abstraction is buildable; eighteen months ago it wasn't.
- **A real court order, not a hypothetical, just turned data-retention promises into legal exposure.** *NYT v. OpenAI* discovery forced OpenAI to preserve all output logs indefinitely regardless of consumer-facing deletion settings ([IronCore writeup with court-order link](https://ironcorelabs.com/blog/2026/ai-coding-agents-drawing-the-line/)); the same article documents Anthropic's 30-day retention applying to Claude Code command-line sessions. Security teams at companies with NDAs, customer data, or pre-release IP now have a citable incident, not a vibes-based concern.
- **Anthropic's `inference_geo` launch confirms enterprises will pay a premium for verifiable data-handling guarantees, even when the guarantee is only geographic.** US-only inference is priced at 1.1× standard rates and configurable per request ([Anthropic data residency docs](https://console.anthropic.com/docs/en/build-with-claude/data-residency)). That a frontier lab built and prices a per-request data-residency primitive is the cleanest signal that enterprise demand for *cryptographic* trust receipts (a stronger guarantee on a different axis) is on the same curve.
- **Confidential Computing has an industry analyst with an enterprise-AI urgency narrative for the first time.** IDC's November 2025 white paper for the Confidential Computing Consortium frames TEEs as a "strategic imperative... accelerated by the massive data-processing demands of AI and LLMs" ([IDC paper](https://confidentialcomputing.io/wp-content/uploads/sites/10/2025/11/US53866125.pdf)). The category is moving out of crypto-native edge cases into mainstream enterprise budget lines.

## Who else is doing this

- **First-party hyperscaler agent runtimes** — main player: **[Microsoft Foundry hosted agents](https://devblogs.microsoft.com/foundry/introducing-the-new-hosted-agents-in-foundry-agent-service-secure-scalable-compute-built-for-agents/)**. Others: [AWS Bedrock AgentCore](https://aws.amazon.com/bedrock/agentcore/). Both ship per-session VM isolation as a feature of their managed agent platform — not as a verifiable attestation primitive, and only on their own cloud. Neither emits a receipt the customer's auditors can verify offline against the hardware root of trust; the trust boundary stops at the cloud's own API. A multi-cloud customer needs two integrations and gets two incompatible audit trails.
- **General-purpose confidential-computing platforms** — main player: **[Anjuna](https://aws.amazon.com/ec2/nitro/nitro-enclaves/)** (Anjuna CEO on the AWS Nitro Enclaves page: targets PII, proprietary algorithms, MPC, key/secrets management). Others: [Fortanix](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) (lift-and-shift confidential applications), [Evervault](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) (Evervault Encryption Engine for cryptographic operations on Nitro Enclaves). All target classic data-in-use workloads — payments, key management, MPC. None ship an agent-loop-aware runtime that captures harness version, tool calls, and model endpoints into the attestation document; an enterprise that wants this stack for agents is integrating a generic confidential-VM platform with their agent harness themselves.
- **Crypto-native verifiable agent runtimes** — Secret Network and Oasis Sapphire ship TEE-attested agent execution with on-chain proofs (surfaced via [grok-x-search live discourse, late April 2026](https://x.com/i/status/2051319053109653552)). Real cryptographic substance, but the buyer is a Web3 protocol, the attestation is on-chain, and the stack assumes EVM/blockchain integration the regulated-enterprise buyer does not have and does not want.
- **Cross-cloud agent governance/control planes** — players above the runtime layer (governance, identity, observability) route to whichever first-party compute the customer already has rather than running the agent in attested compute themselves; they don't issue cross-cloud trust receipts.

**Where the opening is**: There is no neutral runtime that both (a) abstracts confidential compute uniformly across AWS, Azure, and GCP, and (b) emits a hardware-rooted attestation document scoped to an *agent session* — binding harness commit, model endpoint, input hashes, and tool calls into one signed artifact. The hyperscalers won't build it because their incentive is to lock the agent runtime to their cloud's trust boundary; the confidential-computing platforms won't build it because their product surface is generic VMs, not the agent loop; the crypto-native projects won't, because their go-to-market is Web3, not enterprise. The whitespace exists because the structural moat is a *cross-cloud, cross-harness, cross-model* attestation schema — explicitly the thing every category leader has a reason not to ship.

## Why us

- **Vincent's recent multi-part write-up on zero-knowledge proofs is directly load-bearing for the attestation-document schema.** The hard part of the receipt is not the TEE measurement (the cloud signs that); it is designing what enterprise auditors will actually accept as proof of "what ran" — which is a cryptography-design problem, not an infra-glue problem. Founders without crypto-design fluency build receipts that pass cloud-vendor review and fail compliance review.
- **Bizdev at an SF time-series-database startup is the right early-stage muscle for this go-to-market.** The buyer profile (platform-engineering leader at a regulated mid-market, six-figure ACV, design-partner-led sales) is the one TSDB infrastructure also lands in.

## Customer & buyer

- **Customer**: platform-engineering team at a regulated mid-market (1k–10k engineers) — financial services, healthcare-adjacent, defense-tech, regulated SaaS — that has internally banned agents from touching private repos or customer data and is losing engineering velocity to that ban.
- **Buyer**: VP Platform Engineering or Head of AI Platform. Budget line is the developer-productivity / agent-platform line, not the security/compliance line. Typical first ACV $80k–$150k year-one, expanding with seat/session growth.
- **Champion**: the staff platform engineer who built the internal agent harness, has open Jiras from product engineers asking for repo access, and has been told "no" by security.
- **ICP test**: (1) has a written internal policy restricting agent access to private code or PII; (2) operates in at least two of AWS / Azure / GCP; (3) has at least one production agent harness already shipping against public/sanitized data and a backlog of asks for the private workloads.
- **Anti-customer**: pre-Series-B startups (no compliance infrastructure to value the receipt), pure-Azure or pure-AWS shops (one of the first-party runtimes will likely satisfy them), and Web3-native protocols (the on-chain attestation projects are a better fit).

## Wedge / where we could enter

The narrowest first move is **the coding-agent path on private repos**, single design partner, single cloud (AWS Nitro because the attestation primitives are most mature). Ship a `sealskin` CLI that wraps Claude Code or OpenAI Codex, runs the session in a Nitro Enclave, brokers the model call, and emits a signed receipt. The buyer's pain is concrete and the artifact is demoable end-to-end in five days.

- **Candidate A** — coding-agent on private repos, single cloud (chosen above). Demo loop: `sealskin run claude` against a private repo, hand the receipt to the customer's security team, watch them verify it offline.
- **Candidate B** — analytics agent against customer-PII warehouses. Larger ACV, but the buyer is data-platform leadership and the harness landscape is more fragmented; harder to land a sharp first design partner.
- **Candidate C** — production-ops / SRE agents touching prod credentials. Highest blast radius unlocked, but security review for prod-write paths is a 12-month sales cycle the wedge can't survive.

What pushes us to A: it's the workload most engineering teams have already tried, banned, and feel the pain of every week — the demand is pre-existing. What would push us off A: if first design-partner conversations reveal the *attestation* isn't what the security team needs to unblock — if their actual blocker is data-retention policy, not execution-trust, the wedge is misframed.

## What makes it defensible

- **(a) Primary: a cross-cloud, agent-loop-aware attestation schema with a transparency log that customers' auditors learn to recognize.** Every additional engagement adds verified harness fingerprints, model-endpoint registrations, and accepted compliance mappings to a corpus that no first-party hyperscaler can reproduce without ceding cross-cloud neutrality. The moat compounds with customers, not with us.
- **(b) Secondary: harness-integration depth across the agent SDKs that matter** (Claude Agent SDK, OpenAI Agents SDK, LangGraph, Microsoft Agent Framework). Each integration captures harness-specific signal (tool-call boundaries, retry semantics, intermediate-state hashes) that a generic confidential-VM platform doesn't see and that the receipt needs.
- **(c) Year-3 endgame: become the de facto schema for "what an agent did" the way SBOM became the schema for "what a binary contains."** If three or more compliance frameworks (SOC 2 AI addendum, NIST AI RMF, EU AI Act technical-controls guidance) reference the schema, the moat is the standard, not the product.

## How it could make money

| Layer | Price range | Comparable |
| --- | --- | --- |
| **Layer 1: per-session attestation runtime** (per-session compute markup over raw confidential-VM cost) | $0.50–$5 / session | [AWS Nitro Enclaves underlying compute](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) (no enclave premium; charged at base EC2 rates), so all margin sits in the schema and tooling layer |
| **Layer 2: enterprise platform tier** (unlimited sessions, harness/model integrations, transparency log, compliance mappings) | $80k–$300k / yr | [Anjuna platform](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) (enterprise confidential-computing platform on Nitro Enclaves) |
| **Layer 3 (later): regulated-data residency add-on** (per-token premium for inference-routed-through-enclave, multi-region pinning) | 1.05×–1.15× model spend | [Anthropic data residency](https://console.anthropic.com/docs/en/build-with-claude/data-residency) (US-only inference priced at 1.1× standard rates) |

Honest caveat: Layer-1 by itself is a thin metering business that the hyperscalers can collapse the day they ship cross-cloud receipts — which is why Layer-2 has to land within the first six customers, and Layer-3 is the venture-scale upside if the schema becomes the standard.

## What would pressure the thesis

1. **Assumption: enterprise security teams will accept a cryptographic receipt as a substitute for "the data never left our boundary."**
   - **What would pressure it**: design partners say their CISO will only sign off on agents running on-prem or in a customer-VPC enclave they control end-to-end, not in a third-party-managed enclave with a receipt.
   - **Lever**: pivot to BYO-enclave deployment — Sealskin runs as a control plane the customer hosts in their own account, and we sell the schema, transparency log, and harness integrations as the SaaS layer. ACV drops; defensibility shifts further onto the schema.
2. **Assumption: Microsoft and AWS won't ship cross-cloud attestation receipts within 24 months.**
   - **What would pressure it**: a Foundry or Bedrock release that emits a hardware-rooted, vendor-neutral receipt verifiable against AWS/Azure/GCP roots of trust — which would be a genuine business decision against their platform-lock-in incentives but is not impossible.
   - **Lever**: race to make the *schema* the standard before either ships their version. If the schema is recognized by SOC 2 / NIST AI RMF guidance first, the hyperscalers' receipts compete on our format and the moat survives the feature parity.
3. **Assumption: the bottleneck for enterprise agent adoption on sensitive data is execution-trust, not data-retention policy.**
   - **What would pressure it**: design-partner conversations reveal that the security team's actual block is "Anthropic still keeps the request for 30 days regardless of where it ran," not "we can't prove what ran."
   - **Lever**: bundle the receipt with a data-handling guarantee — a contractual ZDR layer in front of the model call, brokered through the enclave so the receipt also covers the retention boundary. Adds vendor-relationship complexity but addresses the actual buyer pain.

## 2-week experiment

**Load-bearing assumption to test**: a platform-engineering leader at a regulated mid-market will, after seeing a working receipt verified offline by their own security team, commit to a paid pilot specifically because the receipt unblocks coding-agent use on private repos.

**Artifact to build (week 1)**: a working `sealskin run` CLI that wraps Claude Code, runs the session inside a real AWS Nitro Enclave, brokers the model call through the enclave, and emits a signed attestation document containing: enclave measurement (PCR hash), harness git SHA, model endpoint URL, SHA-256 of the inputs, and the tool-call sequence. Plus a `sealskin verify` companion that takes the document and validates it offline against AWS's Nitro public root and Sealskin's local transparency log. Five-minute screencast of the full loop on a real (open-source) repo, public on GitHub. Vincent solo with coding agents, ~30–35 hours.

**Conversations (week 2)**: 8 named platform-engineering leaders at regulated mid-market companies (target list: 2 fintech, 2 healthcare-adjacent SaaS, 2 defense-tech, 2 regulated AI infra). Source via warm intros first, cold outbound to fill the rest. Each conversation opens with the screencast and the live `sealskin verify` against their own auditor's machine.

**Specific questions / asks** (each answerable in 30 minutes with the artifact in front of them):
1. Does your security team currently allow agents to read private source? If no, what's the policy citation?
2. If we showed your security lead this receipt, would they accept it as evidence sufficient to lift that ban for a pilot?
3. Which clouds are your agent harnesses deployed against today? Which would need to be supported on day one?
4. Which agent SDKs / harnesses are in production? (We need to know which integrations to ship first.)
5. Is the right buyer for this you, your security counterpart, or a joint approval?
6. Would you sign a paid 6-month pilot at $30k contingent on the receipt being accepted by your auditor?

**Pass criteria**: ≥3 design-partner LOIs at $20k+ each, AND ≥1 buyer puts a PO date in writing, AND the public artifact gets ≥30 GitHub stars or ≥3 inbound replies from platform-eng leaders we didn't cold-outreach.

**Kill criteria**: <2 LOIs after 8 conversations, OR ≥4 of 8 buyers explicitly say their security team needs on-prem deployment that Sealskin's third-party-managed-enclave architecture can't satisfy, OR ≥2 buyers say their actual blocker is data-retention policy at the model layer (which Sealskin doesn't address) rather than execution-trust.

**Vincent's effort**: ~35 hrs build + ~25 hrs conversations = ~60 hrs across 2 weeks. Output: the public CLI + screencast, a memo with quoted answers from all 8 conversations, and a go / pivot / kill recommendation.

## What we don't know yet

- Whether the receipt schema needs to extend to cover *the inference call itself* (i.e., did Claude actually run, on the model claimed) — a meaningfully harder problem since the cloud's TEE doesn't sign what happens inside Anthropic's data center. If yes, Layer-3 becomes load-bearing earlier and the engineering surface grows.
- Whether enterprise auditors will accept a Sealskin-operated transparency log, or insist on a customer-controlled append-only log (Sigstore-style or similar). Determines whether the SaaS moat is the schema + log, or the schema alone.
- The realistic per-session compute overhead and cold-start cost of attested-VM agent sessions at scale — Foundry advertises "predictable cold starts" at seconds; we need to confirm Nitro Enclaves can match that for short-lived agent sessions.

## Vincent's Feedback

*(Vincent fills this in after reading. Reactions, decisions, next moves.)*

## Related

- [[Hallmark — Cryptographic agent-attestation gateway that lets enterprise APIs serve verified agent traffic and bill it correctly]]
- [[Whisper — ZK attestation layer for agent-to-API calls so agents prove eligibility without leaking PII]]
- [[Veritrace — Cryptographically-attested eval logs that turn enterprise AI compliance from a PDF into a proof]]
- [[Foreman — OSS coding-agent fleet scheduler for regulated enterprises]]
