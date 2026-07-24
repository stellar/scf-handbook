---
description: >-
  The RFP (Request for Proposals) Track funds developer tooling that solves
  known problems in the ecosystem. These submissions must align with an active
  SCF RFP.
---

# RFP Track

#### ✅ Who This Track Is For:

* Devs and teams building tools, SDKs, APIs, explorers, or testing infra
* Experienced builders solving problems for other developers

#### 🚫 Who This Track Is Not For

*   Builders without much prior experience in domain or the Stellar ecosystem

    → Better fit for [Instawards](../instawards/)
* Teams building apps, protocols, or integrations for end users\
  → Consider either the [Open Track ](open-track.md)or [Integration Track](integration-track/), depending on your focus
* Teams proposing a tooling idea not aligned with an [active RFP](rfp-track.md#current-open-rfps)\
  → Wait for a future RFP that matches your concept

#### 📋 Requirements

* The submission must address an [open RFP](rfp-track.md#current-open-rfps) from the current quarter—read the RFP carefully and respond directly to its needs.
  * Your proposal does not need to address all points of the RFP, but you should articulate reasoning for a limited scope.
* You must clearly show:
  * Why you’re a good fit to solve this (provide examples of past dev-focused work, and share open-sourced repos if possible)
  * What makes your solution technically strong
  * Clear, testable milestones
  * How your tool will be maintained post-launch
  * A high-level visual diagram (Mermaid or similar) and a plain-English explanation of the technical stack.
* Provide a clear explanation on how your project will be decentralized—if not, why?
* Explain what infrastructure the project runs on.
* Provide an explanation of plans for user tracking and efforts to limit and protect users
* Commitment to regularly updating the community on project status
* Your project should use the most recent stable release of the Stellar tech stack
* Include licensing scheme and commitment to building in the open
  * Consider using Open Source Software like Matrix and decentralized networks (Mastodon / BlueSky) to communicate with your audience

#### Current Open RFPs

_**July 23, 2026: New Q3 RFPs are open for submissions for SCF #**_**45! More coming soon.**

RFPs are sourced from ideas submitted by the Stellar ecosystem, selected by Delegates through the [SCF Quarterly Process](quarterly-governance-process.md), and published here at the start of each quarter:

<details>

<summary>Stellar-compatible LayerZero DVN</summary>

### Stellar-compatible LayerZero DVN

#### 1. Scope of Work

Fund one or more teams already operating production DVNs on LayerZero V2 to extend their verification service to Stellar. The deliverable is a Stellar-deployed DVN contract plus the corresponding off-chain verifier infrastructure, configured to verify LayerZero messages on Stellar pathways and accept attestations to Stellar's ULN302 message library. The expected outcome is that applications building omnichain assets and applications across Stellar and other LayerZero-supported chains have a meaningful choice of independent DVNs to compose into their Security Stack -- involving more DVNs improves security.

#### 2. Background & Context

LayerZero V2 is an omnichain messaging protocol that connects 80+ blockchains. At the core of its security model are Decentralized Verifier Networks (DVNs) -- independent entities that pick up the PacketSent event on a source chain, verify the message hash using their own security logic (ZK proof, TEE, K-of-N consensus, native bridge, light client, or other), and submit an attestation to the destination chain's message library. Applications choose any number of DVNs to compose into their Security Stack under an X-of-Y-of-N model. There are currently 60+ DVNs in the marketplace, including teams like Polyhedra, Google Cloud, Blockdaemon, Nethermind, P2P, FCAT, and LayerZero Labs.

LayerZero V2's Stellar implementation has been built on Soroban in Rust and is currently undergoing multiple security audits (see [Code4Rena audit, April 2026](https://code4rena.com/audits/2026-04-layerzero-stellar-endpoint)). The Stellar implementation preserves LayerZero's four-step messaging flow (Send -> Verify -> Commit -> Execute) and uses the Abstract Account pattern for DVN and Executor contracts to work within Soroban's reentrancy prohibition. At least one reference DVN (LzDVN with secp256k1 multisig) is in place, but for Stellar to be a credible omnichain destination, the LayerZero DVN marketplace on Stellar needs additional independent verifiers.

Why this matters for Stellar in 2026: stablecoins, RWAs, and institutional assets increasingly require cross-chain mobility. LayerZero is a widely used omnichain messaging layer (USDT0, PYUSD, Ondo's tokenized assets, and many others use the OFT standard for native cross-chain liquidity). Leading asset issuers such as USDT0, Paxos, BitGo, Solv, and Ethena are preparing to launch on Stellar via LayerZero, and additional DVN providers can be an important resource to these companies. For Stellar-native assets to participate in this liquidity, and for assets from other chains to settle on Stellar with predictable security guarantees, applications need to be able to choose from multiple DVNs on Stellar pathways -- the more diverse the selection, the better.

Stellar-specific implementation considerations (from the LayerZero V2 Stellar audit notes) that any DVN implementer must address:

* Address format conversion: LayerZero uses fixed bytes32; Stellar uses variable-length addresses. The DVN must handle this conversion correctly.
* TTL-based storage: Soroban storage entries have time-to-live. DVN state (e.g., recent message hashes, signer sets) must use the protocol's hybrid extension strategy to avoid losing critical state to eviction.
* Soroban resource limits: Soroban limits reads to 200 per transaction. DVN attestation flows must stay within this limit -- especially during batch verification -- and more generally must operate within Stellar's current network limits (see [https://lab.stellar.org/network-limits](https://lab.stellar.org/network-limits)) including instruction, memory, and write-entry caps.
* No reentrancy: Soroban prohibits reentrancy. The DVN should use the Abstract Account pattern (custom \_\_check\_auth) rather than self-calls, consistent with the existing LzDVN reference implementation.

#### 3. Requirements

This RFP is intended for teams that already operate a production DVN on LayerZero V2. Greenfield DVN proposals (teams new to LayerZero) are out of scope -- those should be directed to LayerZero Labs directly. Core requirements:

* Existing production DVN on LayerZero V2 -- the team must currently operate a DVN on at least one mainnet pathway, with a track record of message verification visible on LayerZero Scan or equivalent. The Stellar deployment is an extension of an existing service, not a new entity.
* Stellar DVN contract deployment -- a Soroban-based DVN contract deployed on Stellar mainnet (and testnet, in the prior tranche) that conforms to LayerZero V2's DVN interface and the Stellar implementation's Abstract Account pattern. The contract must accept attestations from the team's off-chain verifier and submit them to Stellar's ULN302 message library.
* Off-chain verifier infrastructure for Stellar pathways -- the team's existing off-chain verification service extended to (a) listen to Stellar's RPC for outbound PacketSent events, and (b) submit attestations to destination chains when messages originate on Stellar, and accept attestations from source chains when messages are destined for Stellar. Verification logic should remain consistent with the team's existing service (ZK, TEE, multisig, or other) so applications get a predictable security guarantee across pathways.
* Pathway coverage: minimum viable set -- at submission, the team must commit to supporting DVN pathways between Stellar and at least the top LayerZero chains by total value transferred (Ethereum, Arbitrum, Base, Optimism, Polygon, Avalanche, Solana, BNB Chain). Additional pathway coverage as the team's existing deployments expand.
* Operational commitments -- uptime, message latency, and incident response SLAs consistent with the team's existing DVN service on other chains. The team must commit to maintaining the Stellar deployment for at least 24 months post-launch, with a minimum of 2 nodes in the initial setup.
* LayerZero Labs coordination -- the team must coordinate with LayerZero Labs on integration into the official DVN provider listing and confirm pathway deployment per LayerZero's contract reference. Listing on [docs.layerzero.network/v2/deployments/dvn-addresses](https://docs.layerzero.network/v2/deployments/dvn-addresses) is a hard deliverable.
* Open monitoring -- the team should publish basic operational telemetry (verifications served, error rate, latency p50/p95) on a public dashboard or equivalent so the Stellar ecosystem can independently assess the service.
* Security audit of the Stellar DVN contract -- the Soroban DVN contract must pass a security audit before mainnet activation. Each awarded team is expected to arrange and fund their own audit as part of the grant, since the on-chain DVN implementation is relatively small and scoped. The Stellar Audit Bank remains available for strategic exceptions but is not the default routing.

#### 4. Evaluation Criteria

* Existing DVN track record (hard prerequisite) -- demonstrated production operation of a LayerZero V2 DVN on at least one mainnet pathway, with verifiable on-chain attestation history. Submissions from teams without an existing DVN service will not be considered.
* Verification mechanism quality -- the underlying verification approach (ZK proofs, TEE, K-of-N consensus, light client, or other). Submissions should explain how their mechanism handles Stellar-specific properties (e.g., finality timing, reorg behavior, fee/gas economics).
* Operational reliability -- uptime track record, latency metrics, and incident history from the team's existing DVN deployments. Public metrics or third-party data preferred over self-reported.
* Soroban / Stellar technical capability -- demonstrated ability to ship production Soroban contracts, ideally with a contributor or partner who has shipped on Stellar before. Teams without Stellar experience should describe their onboarding plan and any Stellar engineering partnerships.
* Pathway commitment -- the breadth of LayerZero pathways the team commits to supporting from launch and their stated expansion roadmap. Broader coverage is preferred but not at the expense of operational quality.
* Security and audit history -- prior security audits of the team's existing DVN infrastructure, any historical incidents and their resolution, and a credible plan for the Stellar contract audit.
* Verification mechanism diversity -- the awarded set will explicitly aim for a mix of verification mechanisms (e.g., one ZK, one TEE, one multisig) rather than the top N applicants regardless of mechanism. Mechanism diversity is a security property for OApps composing their Security Stack, and matters to incoming issuers.
* Long-term commitment -- the team's stated commitment to maintain the Stellar deployment beyond the initial 24-month window, including how Stellar pathway operations are funded post-grant.

#### 5. Expected Deliverables

* Soroban DVN contract deployed on Stellar testnet, conforming to the LayerZero V2 Stellar implementation's DVN interface and Abstract Account pattern.
* Off-chain verifier service extended to support Stellar pathways (inbound and outbound), running on the team's existing DVN infrastructure.
* Soroban DVN contract deployed on Stellar mainnet, with security audit complete and findings remediated.
* Listing on LayerZero's official DVN provider directory for Stellar pathways, with documented pathway coverage.
* Public operational telemetry endpoint (verifications served, error rate, latency).
* Documentation: integration guide for OApps that want to include this DVN in their Stellar Security Stack.
* 24-month maintenance commitment, with a stated plan for post-grant sustainability.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

###

</details>

<details>

<summary><strong>Coming Soon</strong></summary>

###

</details>

<details>

<summary><strong>Coming Soon</strong></summary>

###

</details>

If you have an need for a tool or infrastructure that would meet an immediate ecosystem need but isn't listed above, it could be a good idea for an SCF RFP—add it on the [Stellarlight Ideas page](https://ideas.stellarlight.xyz/) and discuss further in the [Stellar Dev Discord](https://discord.gg/stellardev)!

#### 📅 Process & Timeline

1. Submit the SCF Interest form and indicate your interest in the RFP Track.

{% hint style="info" %}
Important: If you were referred by a member of the SCF community, make sure to include their unique referral code on this form.
{% endhint %}

2. Eligible teams will be invited to submit to an upcoming Build round. Submit your Build form before the deadline and choose the RFP Track. In the submission form, clearly identify which open RFP you’re addressing.
3. Submissions are reviewed by 2 reviewers from that quarter’s Category Delegate Panel.
4. If reviewers agree Yes or No, the project moves forward. If reviewers disagree, a third reviewer is added to break the tie. At this stage, teams may be asked to meet with reviewers to go over their submission in more depth.
5. Some teams may receive requested minor changes to their submission before funding.
6. After making any requested changes, awarded submissions receive their first tranche of funding.
7. Once funded, each subsequent tranche must be submitted within 90 days of the previous payment. Teams that miss a deadline without notifying the SCF team in advance forfeit the remainder of their award. See Tranches & Deliverables and the Official Rules for full details.
