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

<summary>X402 Facilitator with Bazaar (discovery) support</summary>

### X402 Facilitator with Bazaar (discovery) support

#### 1. Scope of Work

Build a production ready [x402](https://x402.org/) facilitator for Stellar, running on both testnet and mainnet, shipped under a permissive open source license so it works as a managed hosted provider and as a codebase anyone can fork and self host. Alongside it, build a Stellar native [Bazaar](https://docs.x402.org/extensions/bazaar) discovery layer so agents can find, price, and pay for x402 protected services on Stellar without a pre existing integration.

**Three outcomes define success:**

1. A facilitator other teams can rely on, live on stellar:testnet and stellar:pubnet. Both networks are committed deliverables, not one or the other.
2. A permissive OSI Approved License. The ecosystem must not depend on a single hosted operator.
3. A working Bazaar for Stellar. This is the highest value part of the RFP and should carry the largest share of the budget.

Respondents should build on the Apache-2.0 [@x402/stellar](https://www.npmjs.com/package/@x402/stellar) package rather than reimplement verify and settle. Settlement on Stellar is largely solved; the novel work is discovery, the agent facing interface, the upto scheme upstream, and conformance that holds as the spec moves.

**Deliverable Categories:**

* Offchain service components (facilitator verify and settle, discovery catalog and search index, MCP discovery server)
* Upstream contribution to the x402 package: Stellar support for the upto payment scheme
* Tooling / SDK support (seller helpers for discovery metadata, buyer and agent helpers for querying the Bazaar)
* Documentation
* Integration examples
* Audit readiness

### 2. Background & Context

x402 turns HTTP 402 into a machine native payment flow: a client requests a resource, the server replies 402 with terms, the client signs a payment authorization and retries, and a facilitator verifies and settles onchain before the resource is returned. The buyer is software, typically an agent paying per request with no account or API key.

Stellar suits this well. A settlement costs about 0.0023 XLM, a fraction of a cent, which is what makes per request micropayments viable when the fee would otherwise exceed the payment. USDC, PYUSD, and other stablecoins are first class assets reachable from Soroban through the Stellar Asset Contract. Settlement uses Soroban's authorization model: the client signs an auth entry permitting a specific contract call, and the facilitator submits it and covers the fee.

Stellar already has working exact settlement in several places, including the Apache-2.0 @x402/stellar package and the free public ["Built on Stellar" facilitator](https://developers.stellar.org/docs/build/agentic-payments/x402/built-on-stellar). What it does not have is a native Bazaar. The Bazaar is what turns isolated paid endpoints into something an agent can shop: sellers declare machine readable metadata, the facilitator catalogs any resource carrying the discovery extension, and buyers query a catalog and a search endpoint. Several facilitators run their own Bazaar compatible catalogs, so today a Stellar denominated service is only as discoverable as whichever multi-chain facilitator happens to carry it.

Discovery in x402 is still evolving, and that shapes this RFP. The Bazaar extension was formalized in v2 and the discovery conventions are still moving under the x402 Foundation: endpoint shapes, filters, metadata fields, and cataloging behavior have all changed and will change again. This has two consequences. Respondents are being asked to build against a moving target, so conformance and upkeep are graded as heavily as the initial build (see 3.2 and 3.6). And the work is worth doing now rather than waiting, because the item spec is open, any facilitator may run its own index, and the conventions are being set by the implementations that exist while they are still fluid. SDF is a Premier member of the x402 Foundation with a Governing Board seat, so a bidder does not have to chase spec direction or maintainer review alone.

### 3. Requirements

**3.1 Facilitator**

* Implement x402 verify and settle for Stellar per the current v2 spec and CAIP-2 identifiers, on both `stellar : testnet` and `stellar : pubnet`. Build on @x402/stellar, which already supports both networks.
* Expose the standard surface: verify, settle, and supported.
* Validate Soroban auth entries strictly: correctly signed, authorizing exactly the declared call, asset, amount, and recipient, not replayed, not expired. Support classic keypairs and custom `__check_auth` accounts.
* Support any SEP-41 token, USDC by default, with correct handling of 7 decimal amounts.
* Sponsor network fees so the buyer needs only the payment asset and no XLM, and advertise this correctly via `extra.areFeesSponsored`.
* Be non custodial. The facilitator never takes custody and is never the source of funds. Tampering with a payment must fail signature verification.
* Testnet must be free and usable without friction. Mainnet pricing is the operator's business decision, but any fee must be configurable rather than hard wired so a self hoster can change or remove it. Document the business model.
* Caller authentication, metering, and rate limiting are the respondent's design choice. Document the mechanism and make it configurable.
* Package the hosted and self hosted paths so both are straightforward, including [self facilitation](https://github.com/x402-foundation/x402/tree/main/examples/typescript/servers/self-facilitation) inside a resource server.

**3.2 Bazaar discovery layer**

The core new capability. Submissions should reference specific spec behaviors, not just cite the extension.

* `GET /discovery/resources` for paginated catalog browsing, with the spec's `type`, `payTo`, `network`, `extensions`, `limit`, and `offset` filters.
* `GET /discovery/search` taking a natural language `query`, with cursor pagination and the `partialResults` flag. Search quality is a deliverable, not a detail: this means real ranking, and submissions must describe both their retrieval approach and how they will evaluate result quality over time. It is the hardest part of the scope and the part existing catalogs most often leave unimplemented.
* Automatic cataloging. When the facilitator receives a PaymentPayload carrying the discovery extension, it validates `info` against the supplied `schema` and catalogs the resource with no separate registration step. Manual registration may exist as a secondary path only, since anything requiring a seller to act after payment gets skipped.
* Catalog both HTTP endpoints and MCP tools. The spec treats MCP tools as a first class resource type, keyed on the tuple of `resource.url` and `input.toolName`.
* Enforce catalog integrity. The facilitator is a trust boundary: clients echo the `resource` block into the payment payload, so a hostile client can attempt to poison the catalog with forged service metadata or a crafted `routeTemplate`. Implement the spec's soft drop validation and validate `routeTemplate` including percent decoding before traversal checks.
* Report cataloging outcomes via the `EXTENSION-RESPONSES` header, so a seller can tell whether a listing landed and why not.
* Track the spec as it changes. The catalog, search, and cataloging behavior must follow the x402 discovery conventions as the Foundation evolves them rather than freezing on the award date. Submissions must say how they will monitor spec changes and ship conformance updates, and commit to doing so through the grant period.
* Interoperate with the wider x402 discovery ecosystem. Stellar listings should be representable consistently with how other facilitators represent theirs, so Stellar is not a walled garden.
* Seller side helpers so a resource server can declare discovery metadata correctly, including per parameter descriptions that make an endpoint legible to an agent, with minimal boilerplate.
* Keep the index off-chain by default. An onchain Soroban registry is an optional stretch, not a baseline: it adds rent that must be extended or entries are evicted, and per payment anchoring adds a second transaction that roughly doubles settlement cost. If proposed, respondents must say who bears that cost and keep it off the per payment hot path.

**3.3 Agent facing MCP interface**

* An MCP discovery server that lets an agent search the Stellar Bazaar and make a paid call from inside an agent runtime, wrapping the discover, pay, retry loop behind MCP tools (for example a resource search tool and a paid call proxy).
* Structured, deterministic inputs and outputs, with machine readable error codes. Every rejection carries a non null reason so an agent can reason about failure instead of parsing prose.

**3.4 Settlement schemes: exact and upto**

* `exact` is already specified for Stellar in [scheme\_exact\_stellar.md](https://github.com/x402-foundation/x402/blob/main/specs/schemes/exact/scheme_exact_stellar.md) and must be supported.
* [upto](https://github.com/x402-foundation/x402/blob/main/specs/schemes/upto/scheme_upto.md) (authorize up to a cap, settle actual usage) is the fit for metered services such as token billing. It has EVM and SVM implementation specs but no Stellar one, so this work includes authoring `scheme_upto_stellar.md` as well as the implementation, contributed upstream so the whole ecosystem benefits. Describe how it composes with Stellar smart account spending policies to keep an agent inside a budget. Respondents must state whether their upto design ships a Soroban contract. SEP-41 allowances alone (approve / transfer\_from) cannot enforce the recipient binding and single-settlement guarantees the upto spec requires so a contract-free design must document its weaker trust model explicitly.
* Coordinate the upstream contribution through the x402 Technical Steering Committee. SDF's board seat is available to unblock maintainer review.
* `batch-settlement` is named as planned phase two work, not part of this grant, since on Stellar it needs a Soroban escrow contract, a voucher store, double spend prevention, and its own audit. `auth-capture` is also deferred, as `upto` covers the metered case. Do not foreclose either.

**3.5 Stellar specific considerations**

Submissions should show they understand these, not just name them.

* Auth entries, not pre signed transactions. The facilitator builds and submits the invocation, and the buyer's wallet must support auth entry signing.
* Ledger based expiration. Validity is bounded by `signatureExpirationLedger`, roughly 12 ledgers or 60 seconds by default, derived from `maxTimeoutSeconds`.
* Trustlines. An account needs a trustline to a SEP-41 asset before it can receive it. Onboarding and examples must account for this. See AHA Labs’ Trustline Onboarder RFP
* Soroban resource limits. Verify, settle, and any registry operations must stay within per transaction read, write, instruction, and memory limits.
* Throughput. Agent traffic is bursty. Describe how sequence number bottlenecks are avoided under load, for example channel accounts.
* TTL. If an onchain registry is included, its entries need a rent and extension strategy. The per request schemes hold no persistent onchain state, so this applies only to an optional registry.

**3.6 Non-functional requirements**

* **A Permissive OSI Approved License.** Every dependency must be compatible with permissive redistribution and with operating the code as a network service. No AGPL or other strong copyleft in the dependency path: notably the OpenZeppelin Relayer, its x402 plugin, and the relayer SDK are AGPL-3.0-or-later and are out as a base. Confirm dependency licenses and flag anything uncertain.
* **Conformance is a hard acceptance criterion.** Correct settlement plus a non conformant wire format produces an unusable service, so acceptance is tested at the wire level. Reviewers will point stock SDK code at the deliverable rather than read a conformance claim. Acceptance requires an unmodified canonical client completing a payment end to end on both networks, `/supported` emitting the Stellar extra contract including `areFeesSponsored`, the spec `payload: {transaction}` format accepted verbatim, a passing run of the x402 repo's [e2e suite](https://github.com/x402-foundation/x402/tree/main/e2e) for both networks, a published settled transaction hash per network per scheme, and a non null reason on every rejection.
* **Security.** Strict payload verification, a settlement path resistant to replay and front running, and a discovery index that does not let anyone spoof another seller's listing or pricing.
* **Audit via the** [**Audit Bank**](../../supporting-programs/audit-bank/)**.** A third party security review before the mainnet production tag, covering the settlement path, auth entry validation, the discovery trust boundary, and any registry contract. For costing: v1 ships no new Soroban contract, so this is a review of an offchain service and its cryptographic validation rather than a full contract audit.
* **UX.** A developer should get from docs to a paid, discoverable endpoint appearing in the Bazaar in well under an hour.
* **Performance and availability.** Discovery queries are fast lookups, verify and settle latency suits interactive agent use, public endpoints target 99 percent or better uptime, with a stated story for degraded settlement or indexing.
* **Maintenance.** State how conformance is maintained after the grant, for example a maintenance commitment or a clean handoff so the community can keep it current.

### 4. Evaluation Criteria

* **Technical capability.** Demonstrated understanding of the x402 v2 spec, the Bazaar extension, and Soroban's authorization model. Reference specific behaviors (discovery filters, `routeTemplate validation`, `areFeesSponsored`, auth entry expiration), not just the protocol.
* **Discovery design.** A concrete design for catalog, search, and automatic cataloging, a real answer on natural language search quality and how it is evaluated, and a credible interoperability story.
* **Conformance discipline and upkeep.** Evidence the team treats wire level conformance as first class, plus a plan to stay current as the discovery conventions evolve. Prior conformance runs, spec contributions, or interop bug reports are strong signals. Drift, not inability, is the failure mode this screens for.
* **Relevant experience.** Payment infrastructure, API gateways or facilitators, agent tooling such as MCP servers, or Soroban contracts. Teams that have shipped against x402 are a strong signal.
* **Security and audit history.** A track record of shipping audited infrastructure and clear threat modeling, given this handles real payments.
* **Ecosystem alignment.** Willingness to build on @x402/stellar, coordinate with SDF and the teams behind existing Stellar facilitator work, contribute upto upstream, and align with wallet teams on auth entry signing.
* **Ability to deliver within the required timeline,** with a coherent plan for how sellers and agents actually adopt this alongside existing Stellar x402 tooling.

### 5. Expected Deliverables

* Open source, permissively licensed, self hostable x402 facilitator for Stellar (verify, settle, supported) on both testnet and mainnet, built on @x402/stellar, packaged as a managed provider that others can also fork or self facilitate.
* Stellar Bazaar discovery layer: `GET /discovery/resources` with the spec's filters, `GET /discovery/search` with working natural language ranking, and automatic cataloging for both HTTP and MCP resources.
* MCP discovery server exposing search and paid call tools to agents.
* upto scheme merged upstream into the x402 package with its `scheme_upto_stellar.md` network spec.
* SDK and helper libraries: seller side discovery metadata helpers, buyer and agent side helpers for querying and paying.
* Conformance report: e2e results for both networks, settled transaction hashes per network per scheme, and a demonstration of an unmodified canonical client completing a payment.
* A role based developer guide modeled on the [Algorand x402 developer hub](https://algorand.co/agentic-commerce/x402/developers), organized around what the reader is building, with at least a seller path, a buyer and agent path, and an operator path. Each links live testnet examples so a developer can run the flow. Contributed to Stellar Developer Docs.
* At least two end to end example integrations, for instance a paid API that becomes discoverable and gets paid by an agent, and an MCP driven agent that discovers and pays with no pre baked integration.
* Test suite covering verification, settlement (`exact` and `upto`), discovery, and the MCP interface.
* Security review report with resolved findings.
* Production ready service with an operational runbook and monitoring.

### Appendix: References

**Specs.** Protocol repo and SDKs: [https://github.com/x402-foundation/x402](https://github.com/x402-foundation/x402). Bazaar extension: [specs/extensions/bazaar.md](https://github.com/x402-foundation/x402/blob/main/specs/extensions/bazaar.md). Schemes: [scheme\_exact\_stellar](https://github.com/x402-foundation/x402/blob/main/specs/schemes/exact/scheme_exact_stellar.md), [upto](https://github.com/x402-foundation/x402/blob/main/specs/schemes/upto/scheme_upto.md), and [others](https://github.com/x402-foundation/x402/tree/main/specs/schemes) for context. Facilitator paths: [https://docs.x402.org/core-concepts/facilitator](https://docs.x402.org/core-concepts/facilitator).

**Build on this.** [@x402/stellar](https://www.npmjs.com/package/@x402/stellar), Apache-2.0, supports both Stellar networks. [stellar/x402-stellar](https://github.com/stellar/x402-stellar) has SDF's tools, examples, and a reference facilitator example.

**Do not use.** The free [Built on Stellar facilitator](https://developers.stellar.org/docs/build/agentic-payments/x402/built-on-stellar) runs exact on both networks via the [OpenZeppelin Relayer x402 plugin](https://docs.openzeppelin.com/relayer/guides/stellar-x402-facilitator-guide). Unusable code base to use or study: AGPL-3.0-or-later, and AGPL's network clause applies to a service serving third parties. See 3.6.

**Conformance baseline.** The public x402.org facilitator supports `stellar:testnet` with no API key and correctly returns `extra: {areFeesSponsored: true}`. Any behavior this RFP requires should be verifiable by pointing the same stock client at both it and the deliverable. Respondents are encouraged to test existing multi-chain facilitators the same way before proposing, since advertised support and reachable support are not the same thing.

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
