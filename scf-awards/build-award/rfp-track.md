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
  →  Wait for a future RFP that matches your concept

#### 📋 Requirements

* The submission must address an [open RFP](rfp-track.md#current-open-rfps) from the current quarter—read the RFP carefully and respond directly to its needs.&#x20;
  * Your proposal does not need to address all points of the RFP, but you should articulate reasoning for a limited scope.&#x20;
* You must clearly show:
  * Why you’re a good fit to solve this (provide examples of past dev-focused work, and share open-sourced repos if possible)
  * What makes your solution technically strong
  * Clear, testable milestones&#x20;
  * How your tool will be maintained post-launch
  * A high-level visual diagram (Mermaid or similar) and a plain-English explanation of the technical stack.
* Provide a clear explanation on how your project will be decentralized—if not, why?&#x20;
* Explain what infrastructure the project runs on.&#x20;
* Provide an explanation of plans for user tracking and efforts to limit and protect users
* Commitment to regularly updating the community on project status
* Your project should use the most recent stable release of the Stellar tech stack&#x20;
* Include licensing scheme and commitment to building in the open
  * Consider using Open Source Software like Matrix and decentralized networks (Mastodon / BlueSky) to communicate with your audience

#### Current Open RFPs&#x20;

_**May 11, 2026: New Q2 RFPs are open for submissions for SCF #**_**43!**

RFPs are sourced from ideas submitted by the Stellar ecosystem, selected by Delegates through the [SCF Quarterly Process](quarterly-governance-process.md), and published here at the start of each quarter:

<details>

<summary><strong>Trustline onboarder</strong></summary>

### Trustline onboarder

_Added: Q2 2026_

#### **1. Scope of Work**

Develop a standard (with reference implementation) that enables exchanges, brokers, and wallets to onboard users into Stellar assets without requiring manual trustline setup. The solution should either (a) authorize trustlines on behalf of users via a standard interface, (b) use a temporary intermediate account that auto-configures trustlines, or (c) auto-generate a claimable balance so recipient accounts receive funds without prior trustline setup. A public-facing landing page ("Welcome to Stellar" / activate-assets flow) is in scope as part of the reference implementation.

#### **2. Background & Context**

CEXes and institutional partners (e.g., Societe Generale working with Bitpanda) consistently struggle to let users withdraw native Stellar assets because the trustline requirement creates unintuitive UX—users receive prompts from their wallet or exchange to "create a trustline" without context, which blocks withdrawal flows. With classic assets on Stellar (not Soroban), issuers cannot be MiCA-compliant without an authorization layer. This friction is a recurring blocker for asset issuers launching on Stellar and for exchanges that need predictable withdrawal UX. Existing tools (e.g., Stellar Light, eurcv.theaha.co) point to the shape of the solution but no standard exists. CAP-73 (authorize trustline) is relevant prior art.

#### **3. Requirements**

The RFP should define a standard—plus reference implementation—that addresses the trustline onboarding problem. At minimum, submissions should cover:

* A well-defined standard for trustline authorization (leveraging CAP-73 or an equivalent approach) that custodians, wallets, exchanges, and asset issuers can implement predictably, supporting a full institutional asset lifecycle.
* A reference implementation that demonstrates the standard end-to-end, including the issuer-side authorization flow and the recipient-side activation flow.
* A default landing page flow for brokers, CEXes, and similar platforms where users are redirected to activate assets (akin to eurcv.theaha.co) -- open source and customizable.
* Alternative mechanism support: submissions may additionally propose temporary intermediate accounts with pre-configured trustlines, or automatic claimable-balance creation when a transfer arrives at an un-trustlined account.
* MiCA compliance considerations: the authorization layer should make it possible for regulated issuers to meet MiCA requirements for classic assets.
* Open source (full repository, permissive license).

#### **4. Evaluation Criteria**

Technical capability—experience with Stellar operations, CAP standards authoring or implementation, and wallet/exchange integration patterns.

* Relevant experience -- prior work on asset onboarding, account setup, or authorization flows in Stellar or comparable ecosystems.
* Ecosystem alignment -- willingness and ability to coordinate with custodians, wallet providers, exchanges, and issuers, as well as DeFi protocols during the design phase.
* Standard quality -- clarity, completeness, and adoptability of the proposed standard.
* Ability to deliver within the required timeline.
* Coherent integration plan -- concrete commitments from at least one wallet and one exchange/broker to adopt the reference implementation.

#### **5. Expected Deliverables**

* Published standard (CAP or SEP, as appropriate) with rationale and reference flows.
* Reference implementation: issuer-side authorization tooling and recipient-side activation UI ("Welcome to Stellar" landing page).
* SDK or libraries for wallets and exchanges to integrate.
* Documentation and integration guide.
* Test suite.
* Example integrations with at least one wallet and one exchange/broker.
* Production-ready version.

</details>

<details>

<summary><strong>Passkey UI</strong></summary>

### Passkey UI

_Added: Q2 2026_

#### 1. Scope of Work

Develop a documented set of passkey usage patterns for Stellar smart accounts, paired with a minimal, composable passkey SDK and a small set of reference UI components. The highest-value deliverable is documentation of what works reliably across devices, browsers, and hardware, what breaks, and what fallbacks wallets should use—with the SDK and reference code built around those findings rather than the other way around. The SDK is explicitly intended to be adopted into stellar-wallet-kit so wallet teams can integrate passkey-based authentication for Soroban smart accounts without building UI or compatibility logic from scratch.

#### 2. Background & Context

Passkey-based authentication is a key unlock for user-friendly Soroban smart accounts, but today every team building with passkeys on Stellar (e.g., Stellar Passport from Bastian) is building UI from scratch. Existing reference material (kalepail/smart-account-kit and similar repos) is functional but monolithic—teams report that these kits include too much surface area and are difficult to extract a minimal, composable layer from.

Community feedback in the SCF Pilots discussion is that the ecosystem needs a minimal, neat SDK rather than another big repository, and that the hard part is less about the interface and more about reliable usage patterns across devices, browsers, and hardware. Ishan's framing on this: "the highest-value deliverable is documenting what works reliably, what breaks, and what fallbacks wallets should use." Without that body of knowledge codified somewhere, every new wallet team rediscovers the same compatibility gotchas independently.

The deliverable is explicitly positioned to be adopted into stellar-wallet-kit. Ishan's reasoning: if these passkey primitives had been in stellar-wallet-kit from the start, ecosystem adoption would have been significantly higher. Building the SDK with that integration as a hard requirement avoids the risk of shipping something technically sound but not actually used.

#### 3. Requirements

The deliverable is deliberately small-scoped, with deliverables ordered by value: documentation first, SDK and UI components built around the documentation's findings. Core requirements:

* Usage-pattern guide and compatibility matrix (highest-priority deliverable) -- a documented body of knowledge covering the main device / browser / hardware variability cases: what works reliably, what doesn't, and recommended fallbacks. Web at minimum (Chrome, Safari, Firefox); mobile guidance where passkey support diverges. This is the load-bearing deliverable -- the SDK and UI components are built to embody its conclusions.
* Minimal passkey SDK -- narrow API surface, no bundled opinions on framework, state management, or wallet architecture. The SDK should distill the useful passkey/account pieces from existing work (including kalepail/smart-account-kit and his other passkey kit, where appropriate) into a minimal composable layer that wallet teams can actually adopt.
* Reusable UI components for the common passkey flows (create passkey, sign transaction, recover), designed to be drop-in for wallets without forcing a design system.
* Integration with stellar-wallet-kit (hard requirement) -- the SDK must be adopted into stellar-wallet-kit, not delivered as a parallel package. This introduces external coordination dependency with the stellar-wallet-kit maintainers, but is necessary to ensure ecosystem adoption rather than building something that sits unused.
* Cross-platform support: web (Chrome, Safari, Firefox) at minimum; mobile guidance where passkey support diverges.
* Open source, permissive license.

#### 4. Evaluation Criteria

* Technical capability -- hands-on experience with WebAuthn / passkeys in production, not just demo code. Demonstrated ability to navigate device / browser / hardware compatibility issues is a strong differentiator.
* Documentation quality -- since the highest-value deliverable is a usage-pattern guide, submissions should describe how they will produce, validate, and maintain that documentation. A pattern guide that goes stale within 6 months is worse than no guide at all.
* Relevant experience -- prior work on wallet UI, SDK design, or authentication flows; a track record of small, well-maintained libraries is a strong signal.
* Ecosystem alignment -- willingness and ability to coordinate with stellar-wallet-kit maintainers (hard requirement -- this RFP cannot be delivered as a parallel package), and with existing wallet teams (Meridian Pay, Freighter, others). Also: willingness to coordinate with Tyler on his passkey kit to avoid duplication.
* API design quality -- the SDK must feel minimal and composable; submissions that propose large frameworks should be weighted lower.
* Ability to deliver within a relatively short timeline.
* Coherent integration plan with stellar-wallet-kit, including evidence of a conversation with the stellar-wallet-kit maintainers about the integration approach.

#### 5. Expected Deliverables

* Usage-pattern guide and compatibility matrix covering device / browser / hardware variability, known issues, and recommended fallbacks. Published in a maintainable format with a clear update cadence.
* Minimal passkey SDK adopted into stellar-wallet-kit (not delivered as a separate npm package).
* Reusable UI components (framework-agnostic or framework-specific -- decision documented with rationale).
* Reference integration demonstrating the SDK in use within stellar-wallet-kit.
* Documentation: API docs for the SDK + usage examples + integration guide for wallet teams adopting it.
* Test suite covering passkey flow correctness across the documented compatibility matrix.

</details>

<details>

<summary><strong>Account Demolisher</strong></summary>

### Account Demolisher

_Added: Q2 2026_

#### 1. Scope of Work

Develop a production-ready Account Demolisher tool that allows users to cleanly close a Stellar account: close open positions (offers, LP stakes, DeFi positions), remove all trustlines, remove existing data entries, remove account extra signers (and change account the thresholds accordingly), optionally claim pending claimable balances, convert all tokens to XLM and merge the account—sending all funds to a target destination (exchange or other wallet). The tool must support both classic Stellar operations and Soroban DeFi protocols (which the existing stellar.expert/demolisher tool does not).

#### 2. Background & Context

Stellar has over 10 million accounts on the network, many of them stale or abandoned ("zombie accounts"). Closing an account cleanly is currently a manual, multi-step process that most users cannot navigate, and CEXes periodically need to help users consolidate or withdraw remaining funds. Also none of major CEXes support ACCOUNT\_MERGE operation, which means that users cannot retrieve the remaining 1 XLM of the base account reserve, these funds are basically frozen on the ledger. An open-source precedent exists (stellar.expert/demolisher/public—built by Orbit Lens) but has not been updated in some time and lacks Soroban support. Given the scale of the problem and the sensitivity of a tool that drains accounts, this RFP should be awarded to a well-known, trusted team, and the RFP assumes the existing open-source code is a starting point rather than a blocker.

#### 3. Requirements

Core requirements for a production Account Demolisher:

* Check for existing sponsorships. An account sponsoring reserves for other accounts cannot be merged.
* Check for multisig on the account - merging an account with multisig requires permissions from several key holders.
* Check current signature scheme and thresholds and remove all extra singers while setting thresholds in a way that will allow further manipulations without permission of other signers.
* Remove all trustlines on a given Stellar account.
* Remove data entries set by account.
* Optionally claim selected claimable balances.
* Close all open positions: DEX offers, AMM / LP stakes, DeFi positions in the main Stellar protocols (Blend, Aquarius, Soroswap, etc.).
* Sell all tokens (classic and Soroban) to a target base asset (XLM or user-specified) via best-available routing.
* A user should have an option whether to send all current funds (if any non-XLM balances remain) to the third-party wallet or exchange.
* Merge the account, sending all remaining funds to a target destination (exchange address or other wallet). The tool should use a temporary mediator account to transfer all remaining funds after the merge (CEXes do not support ACCOUNT\_MERGE operation).
* The tool should provide an option to view active token allowances and retrieve active authorizations without removing the account. This helps users to secure their funds in case of allowance-based DeFi protocol exploits.
* Soroban support -- full parity with classic assets.
* The UI should support stellar-wallets-kit and direct secret key input. Merging multisig accounts might require gathering signatures from several key pairs, so the interface should support adding multiple secret keys or signing transactions with different Stellar wallets.
* This tool should be implemented in a trust-minimization, non-custodial manner. All transactions should be signed on the client side. Secret keys should never be transferred to the server side. The tool should&#x20;
* Safety features: confirmation flows, clear warnings and where possible, a dry-run / preview mode (for most accounts clearing all active entries will require several sequential transactions, so it will be challenging to create a clear dry-run output, would like to see the proposers approach here).
* Open source, permissive license -- existing [stellar.expert/demolisher](http://stellar.expert/demolisher) code can be a starting point.
* Production-grade UX -- this tool handles irreversible actions and must be trustworthy.

#### 4. Evaluation Criteria

* Technical capability -- demonstrated experience with Stellar classic operations, Soroban contract interaction, and DeFi protocol integration.
* Relevant experience -- prior work on account management, DEX routing, or similar destructive-action tooling. Experience with the existing stellar.expert/demolisher codebase is a plus.
* Security & audit history -- given the irreversible nature of account closure, the team must demonstrate a strong security track record.
* Ecosystem reputation -- this tool will be used on real accounts with real balances; submissions from well-known ecosystem teams will be weighted accordingly.
* Ability to deliver within the required timeline.
* Coherent integration plan -- how the tool will be surfaced to users (standalone UI? wallet integration with stellar-wallets-kit? CEX partnership?).

#### 5. Expected Deliverables

* Production-ready frontend (web, at minimum).
* Backend service / using one of the DeFi position API RFP recipients ([Octopos](https://communityfund.stellar.org/dashboard/submissions/recOh9tgSDRC3elBf) and [Orion](https://communityfund.stellar.org/dashboard/submissions/recPt6cTMzx8XmiNj))
* Documentation.
* Test suite, including adversarial / edge-case tests.
* Security audit and remediation (can be done as part of Audit Bank)<br>

</details>

<details>

<summary><strong>Contract Source Verification Service</strong></summary>

### Contract Source Verification Service

_Added: Q2 2026_

#### 1. Scope of Work

Design and deliver a source code verification pipeline for Soroban smart contracts that proves a deployed Wasm was built from a specific, publicly inspectable source tree. Deliverables span:

* Offchain service components: a public verification service that accepts source code submissions (tarballs or equivalent), rebuilds the Wasm in a deterministic environment, and links the resulting Wasm digest to the source artifact.
* Tooling / SDK support: deterministic build tooling (e.g., a standardized Docker image or reproducible build workflow) that contract developers can adopt.
* Integration examples: reference integrations showing how explorers, wallets, and other downstream tools query verification status and retrieve source tarballs.
* Documentation: contributor-facing docs for developers submitting verifications and integrator-facing docs for tools consuming them.
* Audit readiness: threat model, security review, and audit fixes prior to production handoff.

**Explicitly out of scope:**

* Make updates to the existing SEP-55 spec itself (see[ ecosystem/sep-0055.md](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0055.md)). Coordination with SEP-55 evolution is expected.
* Integration of verification metadata into SDF-owned tooling (stellar-cli, Stellar Lab). SDF-owned tooling will consume the RFP service's APIs; building out those integrations is handled in-house. The RFP deliverable must expose the right APIs to make that integration straightforward.
* Explorer UI work on any specific third-party explorer (Stellar Expert, Chain.dev), though the service must expose what they need to consume.
* Fully deterministic Rust compilation as a research effort. The RFP should use the best available reproducibility today.

#### 2. Background & Context

Soroban contracts currently have no way to prove that the source code displayed on explorers actually compiles to the deployed Wasm. The existing SEP-55 mechanism ([merged spec](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0055.md)) relies on GitHub Actions attestations that confirm a workflow ran at a given commit, but the workflow itself can fetch external code, modify dependencies, or otherwise produce a Wasm that diverges from the linked source. The attestation proves build provenance, not source-to-bytecode correspondence.

This gap has been raised repeatedly in the ecosystem:

* SEP-55 spec discussion ([stellar/discussions/1573](https://github.com/orgs/stellar/discussions/1573)): OrbitLens has noted that without a fixed build pipeline, attestation-based verification "provides a false sense of security." The merged v0.4.0 explicitly scopes itself to providing "unfalsifiable evidence that a contract has been compiled automatically using a particular GitHub repository," not that the displayed source matches the deployed binary.
* Post-deploy verification discussion ([stellar/discussions/1802](https://github.com/orgs/stellar/discussions/1802)): tracks ongoing work on alternatives to attestation-based verification.
* Experimental work in progress:[ stellar-experimental/contract-verifications](https://github.com/stellar-experimental/contract-verifications) is an in-house prototype, but has not been built out to production.
* Partner requirement: during launch prep, a major ecosystem partner demonstrated a malicious Wasm receiving "build verified" status while linking to unrelated source code. They cited Solana's foundation-provided Docker image as the model they expected ("makes the bytecode deterministic and doesn't rely on external tooling"). This was the immediate driver for removing the Stellar Lab source code tab ([laboratory/issues/2045](https://github.com/stellar/laboratory/issues/2045)) as a stopgap fix while a real solution is built.
* Complementary CLI work: Leigh McCulloch's proposal ([stellar-cli#2506](https://github.com/stellar/stellar-cli/issues/2506)) adds a --docker option to stellar contract build and a stellar contract verify command. The build records the Docker image digest and CLI version in contract metadata, and the verify command rebuilds from source and compares output. This solves the build reproducibility layer from the cli, but leaves open how verification status gets displayed across explorers, Lab, and wallets without each consumer independently rebuilding every contract or delegating to a single centralized verifier. This RFP fills that gap.
* Internal alignment on boundary: SDF engineering has previously flagged that tooling integration work (stellar-cli, Stellar Lab, and partnerships with explorers) is best handled in-house, while a public service that performs rebuilds and verifications is a natural fit for external funding. This RFP sits on the public-service side of that line.

Downstream effects: explorers can't safely display source code, auditors can't rely on explorer-surfaced sources for review, and ecosystem partners are treating verification as a launch requirement.

Other ecosystems have solved this via services like[ Sourcify](https://sourcify.dev) (EVM), which link deployed bytecode to reproducible source via tarball submission and rebuild. Stellar needs an equivalent that's either adapted from existing tooling or purpose-built for Soroban's toolchain. Respondents may propose either approach.

**Reference links:**

* Post-deploy verification discussion:[ https://github.com/orgs/stellar/discussions/1802](https://github.com/orgs/stellar/discussions/1802)
* SEP-55 spec:[ https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0055.md](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0055.md)
* \[Prototype] Contract Source Verification using Docker without Attestation [https://github.com/orgs/stellar/discussions/1923](https://github.com/orgs/stellar/discussions/1923)
* SEP-55 spec discussion:[ https://github.com/orgs/stellar/discussions/1573](https://github.com/orgs/stellar/discussions/1573)
* Stellar Lab issue:[ https://github.com/stellar/laboratory/issues/2045](https://github.com/stellar/laboratory/issues/2045)
* Reference solutions
  * Stellar CLI reproducible builds proposal:[ https://github.com/stellar/stellar-cli/issues/2506](https://github.com/stellar/stellar-cli/issues/2506)
  * In-house prototype:[ https://github.com/stellar-experimental/contract-verifications](https://github.com/stellar-experimental/contract-verifications)
  * Solana’s solution [https://solana.com/docs/programs/verified-builds](https://solana.com/docs/programs/verified-builds)

#### 3. Requirements

**Functional requirements:**

* Accept source code submissions (tarball or equivalent) tied to a target Wasm hash
* Rebuild the submitted source in a controlled environment and compare the resulting Wasm to the deployed Wasm
* Provide and maintain a controlled environement to build the submitted code.
* Expose a free, public API for querying verification status by contract ID or Wasm hash, returning at minimum: verification status, linked source tarball URL, build metadata, and verification timestamp
* Provide a verification result layer that explorers, Lab, wallets, and other consumers can query without performing their own rebuilds. Verification should be performed once and the result made available via API, so displaying verification status on a contract page is a cheap lookup rather than a full rebuild. This is a hard requirement: solutions that force every consumer to rebuild, or that rely on a single hardcoded verifier, do not meet the bar.
* Support mainnet and testnet
* Handle contracts deployed before verification service launch (retroactive verification for non-upgradable contracts is a priority requirement, given that many existing deployments cannot be redeployed)
* Provide a CLI or developer-facing submission flow so contract authors can verify their own deployments. API should be shaped to allow integration with[ stellar-cli](https://github.com/stellar/stellar-cli)
* Expose verification metadata in a form consumable by explorers (Stellar Expert, Chain.dev,[ Stellar Lab](https://github.com/stellar/laboratory)) and other downstream tools
* Coexist with the existing SEP-55 attestation flow. Attestation-based verification and source-tarball verification should be surfaced as distinct trust levels

**Non-functional requirements:**

* Explain your approach in the post-deploy verification discussion thread:[ https://github.com/orgs/stellar/discussions/1802](https://github.com/orgs/stellar/discussions/1802)
* Security: tarball storage must be tamper-evident; rebuild environment must be isolated from host; submitted code must not be able to exfiltrate secrets or affect other submissions
* Audit: a third-party security audit is required before production launch; audit scope to include rebuild environment, tarball integrity, and API authentication
* UX: a contract developer should be able to verify a deployed contract in under 15 minutes from reading the docs to seeing the verification appear
* Decentralization of verification: the service architecture must allow multiple independent verifier instances to produce and publish results, so consumers aren't forced to trust a single party. Proposals should describe how disagreement between verifiers is surfaced and how a consumer picks a trusted set.
* Performance: verification requests should complete or return a queued status within 5 minutes for standard contract sizes
* Availability: the public query API should target 99%+ uptime
* Compliance: service must be operable as a public good without KYC or gated access; no user data collection beyond what's necessary for abuse prevention
* Openness: the service codebase must be open-source and self-hostable; production deployment should allow for community operation over time

#### 4. Evaluation Criteria

*   Technical capability: demonstrated experience building reproducible build pipelines and verification infrastructure

    Display-layer design: clear answer to how downstream tools (explorers, Lab, wallets) consume verification status without running their own rebuilds
*   Relevant experience: prior work on Sourcify or equivalent services on other chains, or deep Soroban / Rust toolchain experience

    Security & audit history: track record of shipping audited infrastructure; clear threat modeling in the proposal
* Ecosystem alignment: willingness to coordinate with explorer teams (Stellar Expert, Chain.dev), SDF tooling (stellar-cli, Stellar Lab), and the SEP-55 discussion in[ 1573](https://github.com/orgs/stellar/discussions/1573) and[ 1802](https://github.com/orgs/stellar/discussions/1802)
* Ability to deliver within required timeline: realistic milestone plan, not over-promising
* Coherent integration plan: clear story for how explorers and other consumers adopt the service, including API stability guarantees

#### 5. Expected Deliverables

* Verification service codebase, open-source and self-hostable
* Public deployment of the service for mainnet/testnet
* Deterministic build tooling (e.g., reference Docker image or reproducible workflow)
* SDK or client library for querying verification status
* Contract developer CLI or submission interface
* Integration documentation for explorers and downstream tools
* User documentation for contract developers, contributed to Stellar Developer Docs
* Test suite covering verification logic, API, and rebuild environment
* Security audit report and resolved findings (through Audit Bank)
* Production-ready service with operational runbook and monitoring
* At least one reference integration (ideally[ Stellar Lab](https://github.com/stellar/laboratory) or a cooperating explorer)

</details>

<details>

<summary><strong>OZ accounts policy builder</strong></summary>

### OZ accounts policy builder

_Added: Q2 2026_

#### 1. Scope of Work

Develop an AI-assisted toolkit (likely a combination of an MCP server and a Claude / agent skill) that helps developers and end users craft OpenZeppelin smart account policies and context rules from observed or simulated Stellar transactions. The core deliverable is a "record-and-generate" workflow: a user (or agent) executes a representative transaction sequence—for example, claiming yield on Blend and converting it to USDC—and the tool synthesizes a context rule plus the minimum set of policies that would permit exactly that flow, scoped tightly enough that a delegated third party (human or agent) can repeat the operation but cannot deviate from it. The deliverable is positioned as an MCP server / agent skill / developer tool, not a hosted service that auto-deploys policies on behalf of users. The tool generates reviewable policy code; deployment is always a separate, explicit step performed by the user (or by an agent operating under existing permissions).

#### 2. Background & Context

OpenZeppelin's [smart accounts framework](https://docs.openzeppelin.com/stellar-contracts/accounts/smart-account) for Stellar (built on Soroban smart accounts and the OZ accounts package) decomposes authorization into three composable elements: context rules (scope and lifetime bindings, e.g. "call transfer() on USDC for one year"), signers (the entities authorized to act), and policies—enforcement modules that add programmable constraints like spending limits, multisig thresholds, or time windows. A single context rule can attach up to 5 policies, evaluated through a defined lifecycle (install / can\_enforce / enforce / uninstall).

The expressive power of this design is significant: the same primitive supports subscription billing, agent delegation, social recovery, and corporate treasury rails. The tradeoff is authoring complexity. Today, writing a custom policy means writing a Soroban contract that implements the Policy trait correctly, segregates storage by both smart account address and context rule ID (for stateful policies), handles the install/enforce/uninstall lifecycle, and gets audited. That bar is too high for most application developers, and effectively prohibitive for end users who want to delegate a narrow capability to an agent or service.

The most powerful unlock here is letting users start from a transaction they have already performed (or simulated). An AI-assisted toolkit can examine the effects of that transaction—which contracts were called, which functions were invoked, which assets moved, in what amounts, in what order—and from that derive a context rule plus the policies needed to permit a future invocation of that same flow, but only that flow. "Record this sequence, generate a policy that allows exactly this and nothing else."

This sits at the intersection of three priorities for Stellar in 2026: AI / agent-readiness of the network, smart account adoption (C-addresses), and developer experience improvements that make Soroban's expressive capabilities practical to use. The output is also defensively useful—agents acting under tightly scoped policies are categorically safer than agents holding full account keys, which matters as AI agents take on more autonomous on-chain roles.

OpenZeppelin involvement: OZ has been consulted on this RFP and indicated interest in participating as a technical reviewer rather than a co-owner. Design decisions and generated-code quality should be validated with the OZ accounts package maintainers, but the deliverable is independent of OZ's own roadmap.

Prior art: Tyler (kalepail on GitHub) has built [kalepail/pollywallet](https://github.com/kalepail/pollywallet) as a basic MVP demonstrating the core record-and-generate concept in under a week of work. A demo video is available at [https://youtu.be/vmFnCtkqQJA](https://youtu.be/vmFnCtkqQJA). Respondents should treat this as the existing starting point and scope their work around extending it to production-quality (audited synthesizer, MCP server, agent skill, wallet integration) rather than building from scratch.

#### 3. Requirements

The deliverable is a developer/end-user-facing toolkit, not a new contract primitive. At minimum, submissions should cover:

* A transaction recording / observation layer that can ingest either (a) a real on-chain transaction by hash on mainnet/testnet or (b) a locally simulated transaction (e.g., from a Soroban simulation against a forked state). The layer must extract structured information about which contracts were invoked, which functions, with which arguments, and the resulting state changes / token movements.
* A context rule + policy synthesizer that converts the recorded transaction(s) into a proposed context rule (scope: which contracts and functions; lifetime: how long the permission lasts) plus the smallest set of policies needed to constrain the rule (e.g. spending limits derived from the observed amounts, frequency limits, time bounds). The synthesizer should bias toward minimal permissions -- if a transaction sequence only ever calls two functions with two specific assets, the generated rule should not permit a third.
* Generated policy code in Rust, suitable for compilation as a Soroban contract, leveraging existing OZ-provided policy primitives (simple\_threshold, weighted\_threshold, spending\_limit) wherever they suffice. The tool should compose existing policies first and only generate net-new policy contracts when the constraint cannot be expressed by combining standard ones. Where new policy code is generated, it must implement the Policy trait correctly, including proper storage segregation for stateful cases.
* An MCP server that exposes the recording, synthesis, and verification capabilities to agents, so that an AI agent can both request a policy be drafted from a sample transaction and operate under that policy once installed. The MCP interface should be agent-friendly: structured inputs/outputs, deterministic behavior, machine-readable error codes. Get inspiration from the [Cloudflare Agent Setup](https://developers.cloudflare.com/agent-setup/) and how they handle plugins, mcp and skills.
* An Agent skill (or equivalent for other agent frameworks) that wraps the MCP and gives an agent a high-level conversational entry point: "the user wants to grant permission to do X; here is a transaction they performed; draft a policy." The skill should know when to ask for clarification (e.g., "this transaction transferred 50 USDC -- should the policy cap at 50, or allow up to 100 over a week?"). Can be for Claude and similar tools.&#x20;
* A simulation / dry-run harness that tests a generated policy against (a) the original recorded transaction (must permit), (b) a set of adjacent transactions that should be denied (e.g., same operations but different asset, larger amount, or out-of-window timing), so the user can verify the policy is neither too strict nor too permissive before installing it.
* Integration with at least one existing Stellar wallet supporting OZ smart accounts (e.g., a wallet from the C-Address Tooling cohort) so the policy install flow is end-to-end demonstrable: record -> generate -> simulate -> sign -> install on a real smart account.
* Documentation and examples covering at least three end-to-end policy generation walkthroughs from real Stellar use cases (Tyler suggested Blend yield-claim flows; other candidates include subscription billing on a SEP-41 token, delegated trading on Soroswap with bounded slippage).
* Configurable composition / generation mode -- the synthesizer must support both modes: (a) configuring existing OZ policy contracts (simple\_threshold, weighted\_threshold, spending\_limit) where they can express the constraint, and (b) generating fresh policy contracts where they cannot. The user should be able to inspect and modify generated policy code before deployment, not be forced into a fully automatic flow.
* Code-first, deploy-second workflow -- the tool produces human-readable, reviewable policy code as its primary output. Deployment is never automatic. The user (or a separately-authorized agent) reviews the generated code, optionally modifies it, and then deploys it as a discrete step.
* Open source, permissive license.

#### 4. Evaluation Criteria

* Technical capability -- demonstrated experience with Soroban contract development, Rust, and ideally with OpenZeppelin's accounts framework specifically. Prior work building MCP servers or AI tooling is a strong differentiator.
* Relevant experience -- prior projects involving authorization frameworks, account abstraction (Stellar or otherwise), or codegen tooling. Teams that have shipped agent-facing tooling (MCPs, agent skills) will be weighted more heavily.
* Security & audit history -- this tool generates code that runs as authorization logic on user funds. Any team submitting must be able to articulate a clear story for verifying generated policies, including how the simulation harness tests deny-cases, and must commit to an audit of the synthesizer logic itself (not just sample outputs).
* Coordination with OpenZeppelin -- OZ has been consulted on this RFP and indicated interest in participating as a technical reviewer (not a co-owner). Submissions should describe how they will engage OZ as a technical reviewer: sharing design decisions on policy library composition, getting feedback on generated code quality, and aligning on what primitives would be valuable to upstream into the OZ accounts package.
* Ecosystem alignment -- commitment to integrate with at least one existing Stellar smart-account-supporting wallet and to coordinate with the C-Address Tooling cohort.
* Ability to deliver within a relatively short timeline.
* Coherent integration plan -- a clear story for how the toolkit fits into existing developer and agent workflows, not just a standalone demo.
* Building on existing work -- submissions should explicitly address what they will adopt, extend, or replace from kalepail/pollywallet. Greenfield rewrites should be justified.

#### 5. Expected Deliverables

* MCP server (open source) implementing the recording, synthesis, simulation, and verification capabilities.
* Claude skill (or equivalent agent integration) wrapping the MCP server with a conversational interface.
* Policy synthesizer library (Rust + supporting tooling) that produces compilable Soroban policy code.
* Simulation / dry-run harness with permit-case and deny-case test generation.
* Reference integration with at least one Stellar smart-account-supporting wallet, demonstrating the end-to-end record -> generate -> simulate -> install -> use flow.
* Three documented end-to-end walkthroughs (Blend yield, SEP-41 subscription, bounded Soroswap delegation, or equivalents).
* Developer documentation: how to use the toolkit, how the synthesizer makes scoping decisions, how to extend it with new policy primitives.
* Test suite covering the synthesizer's correctness on a range of input transaction shapes.
* Security audit of the synthesizer + generated policy templates, with findings remediated.
* Production-ready release with versioned MCP server endpoint and packaging for the Agent skill (e.g. for Claude + others).

</details>

If you have an need for a tool or infrastructure that would meet an immediate ecosystem need but isn't listed above, it could be a good idea for an SCF RFP—add it on the [Stellarlight Ideas page](https://ideas.stellarlight.xyz/) and discuss further in the [Stellar Dev Discord](https://discord.gg/stellardev)!

#### 📅 Process & Timeline

1. Submit the SCF Interest form and indicate your interest in the RFP Track.

{% hint style="info" %}
Important: If you were referred by a member of the SCF community, make sure to include their unique referral code on this form.&#x20;
{% endhint %}

2. Eligible teams will be invited to submit to an upcoming Build round. Submit your Build form before the deadline and choose the RFP Track. In the submission form, clearly identify which open RFP you’re addressing.
3. Submissions are reviewed by 2 reviewers from that quarter’s Category Delegate Panel.
4. If reviewers agree Yes or No, the project moves forward. If reviewers disagree, a third reviewer is added to break the tie. At this stage, teams may be asked to meet with reviewers to go over their submission in more depth.
5. Some teams may receive requested minor changes to their submission before funding.
6. After making any requested changes, awarded submissions receive their first tranche of funding.

