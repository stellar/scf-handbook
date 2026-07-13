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
* This tool should be implemented in a trust-minimization, non-custodial manner. All transactions should be signed on the client side. Secret keys should never be transferred to the server side. The tool should
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

Design and deliver a public, hosted contract source verification service for Soroban smart contracts. The service consumes the [SEP-58](https://github.com/stellar/stellar-protocol/pull/1933) metadata vocabulary (bldimg, bldopt, source\_repo, source\_rev, tarball\_url, tarball\_sha256), rebuilds submitted source in a defined environment, compares the resulting Wasm to the deployed Wasm, and exposes the result to downstream consumers (explorers, wallets, the CLI). The service must cover both public source (git repo plus commit) and private source (content-addressed via `tarball_sha256` alone, suitable for auditor-mediated rebuilds).

This service sits downstream of an already-shipping foundation. SDF is publishing the trusted stellar-cli-docker image plus "how to build" and "how to verify" guides on a shorter timeline. Asset issuers, contract developers, and planned verifiers (OrbitLens, Aha Labs, 57B) use those directly in the near term. The hosted service this RFP funds aggregates verifications across the ecosystem and serves results to downstream tools.

Deliverables span:

* **Audit readiness:** threat model, security review, and audit fixes prior to production handoff.
* **Offchain service components:** a verification service that accepts source submissions (tarballs or equivalent), rebuilds the Wasm using an SDF-allowlisted trusted build image, and links the resulting Wasm digest to the source artifact.
* **Public API:** a stable, free API for querying verification status by contract ID or Wasm hash. Returns SEP-58 fields plus verification status and timestamps.
* **Integration examples:** reference integrations for explorers, wallets, and other downstream tools.
* **Developer-facing submission flow:** a CLI or web interface so contract authors can submit their own deployments.
* **Documentation:** contributor-facing docs for submitters and integrator-facing docs for consumers
* **Audit readiness:** threat model, security review, and audit fixes prior to production handoff.

**Explicitly out of scope:**

* **Display-layer policy decisions by individual verifiers** (e.g., whether to surface verifications for contracts without publicly retrievable source). The service may expose auditor signals or off-chain attestations if available, but is not required to define their semantics.
* **Authoring SEP-58, SEP-55.** Coordination is expected; authorship is not.
* **Producing the official trusted stellar-cli Docker images.** SDF maintains these via stellar-cli-docker. Vendors consume the SDF-published images.
* **Updates to SDF-owned tooling** (stellar-cli, Stellar Lab) beyond exposing the APIs those tools consume. SDF builds those integrations in-house.
* **Explorer UI work on any specific third-party explorer** (Stellar Expert, StellarChain), though the service must expose what they need.
* **Fully deterministic Rust compilation as a research effort.** Use the best available reproducibility today, anchored on the SDF-allowlisted trusted images.

#### 2. Background & Context

[SEP-58](https://github.com/stellar/stellar-protocol/pull/1933) (Draft, in active review since 2026-05-15) defines the metadata a Soroban contract embeds, or surfaces off-chain, so any verifier with the source can rebuild the Wasm and confirm the bytes match. SEP-58 is a vocabulary. It leaves the service implementation, build infrastructure, and explorer integrations to ecosystem teams. This RFP funds the service layer.

SEP-58 complements [SEP-55](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0055.md), which uses signed CI attestations to bind a workflow run to a commit and a Wasm. SEP-55 asks "did a trusted CI compile this Wasm?". SEP-58 asks "does this source produce this Wasm?". A contract can carry meta supporting both. Verifiers pick whichever path fits their threat model.

Soroban contracts deploy as opaque Wasm bytes. Today, an explorer can display source code linked to a contract, but the connection between that source and the deployed bytes is not protocol-level provable. SEP-58 provides the standard inputs. The remaining work is a service that performs rebuilds and serves results to downstream tools, so each tool doesn't run its own rebuild infrastructure.

SEP-58 is mode-agnostic about source retrieval. Public repos use source\_repo + source\_rev. Hosted tarballs use tarball\_url + tarball\_sha256. Closed-source builds use tarball\_sha256 alone, committing to specific source bytes without naming a retrieval channel (suitable when only an auditor with access can rebuild). What differs between public and private source isn't the spec; it's who rebuilds and which verifiers display the result. Some verifiers (e.g., Stellar Expert) will not auto-verify contracts without publicly retrievable source. The service must support all SEP-58 source modes; downstream display decisions are out of scope.

**Ecosystem context:**

* **Complementary CLI work:** stellar-cli [PR #2585](https://github.com/stellar/stellar-cli/pull/2585) adds `stellar contract build --verifiable`, which runs the build inside a digest-pinned Docker container and stamps SEP-58 metadata into the Wasm. [PR #2586](https://github.com/stellar/stellar-cli/pull/2586) adds `stellar contract verify`, which reads the metadata, re-runs the recorded build, and byte-compares the result. The CLI verifies locally with no service dependency. This RFP funds the shared layer aggregating results across verifiers.
* **Trusted build images:** SDF maintains stellar-cli-docker, which publishes attested Docker images for use as bldimg values. The publish pipeline ([PR #3](https://github.com/stellar/stellar-cli-docker/pull/3)) targets a first published image in late May 2026. It covers public Dockerfiles, SLSA build provenance, SBOMs, pinned base images, and a defined release cadence.
* **Multi-dimensional trust:** reproducibility alone is not faithfulness to source. A hostile image can deterministically rewrite bytes and still pass byte-comparison. The service should treat image trust as a signal (arbitrary deployer image, publicly auditable image, SDF-maintained trusted image), not a binary.
* **Existing in-house prototype:** [stellar-experimental/contract-verifications](https://github.com/stellar-experimental/contract-verifications) is a starting point but is not production-ready.
* **Internal boundary:** SDF builds the CLI, trusted images, and Stellar Lab integrations. The hosted public verification service is a fit for external funding.

Other ecosystems have solved this via [Sourcify](https://sourcify.dev) (EVM) and [solana-verify](https://solana.com/docs/programs/verified-builds). Stellar needs an equivalent, either adapted from existing tooling or purpose-built for Soroban. Respondents may propose either approach.

#### 3. Requirements

**Functional requirements:**

* Accept source code submissions (tarball or equivalent) tied to a target Wasm hash.
* Rebuild the submitted source using an **SDF-allowlisted trusted build image** referenced via SEP-58 bldimg. Vendor describes its image allowlist policy in the proposal.
* Expose a free, public API for querying verification status by contract ID or Wasm hash. Response includes at minimum: verification status, SEP-58 fields recorded (bldimg, bldopt, source\_repo, source\_rev, tarball\_url, tarball\_sha256 as applicable), linked source artifact, build metadata, image trust signal, and verification timestamp.
* Provide a shared verification result layer that explorers, Lab, wallets, and other consumers can query without performing their own rebuilds. Verification runs once and the result is available via API. Hard requirement: solutions that force every consumer to rebuild, or that rely on a single hardcoded verifier, do not meet the bar.
* Support **multi-verifier architecture.** Each verifier reports its result against the deployed Wasm hash. Disagreement surfaces as a per-verifier signal (e.g., \[√] Verified by X, \[!] Mismatching verification by Y), not a single "correct" status.
* Support Mainnet and Testnet.
* Handle contracts deployed before service launch (**retroactive verification for non-upgradable contracts is a priority requirement,** since many existing deployments cannot be redeployed).
* Source retrieval must not hardcode HTTPS or GitHub. The API and rebuild flow accept all SEP-58 source identifier modes: public repo (`source_repo` + `source_rev`), hosted tarball (`tarball_url` + `tarball_sha256`), and content-addressed (`tarball_sha256` alone). **IPFS retrieval is a first-tier channel alongside HTTPS.** Vendors may propose which modes their service handles directly versus surfaces from off-chain sources; the API must distinguish modes in responses.
* Provide a CLI or developer-facing submission flow. API shaped to integrate with [stellar-cli](https://github.com/stellar/stellar-cli).
* Expose verification metadata in a form consumable by explorers (Stellar Expert, StellarChain, [Stellar Lab](https://github.com/stellar/laboratory)) and other downstream tools.
* **Coexist with SEP-55 attestations and SEP-58 rebuild verification as distinct trust levels.** The API distinguishes them.

Conform to the forthcoming verifier-API SEP (currently unauthored, expected to follow SEP-58). Vendor commits to align the API once that spec lands.

**Non-functional requirements:**

* **Explain your approach** in the [SEP-58 discussion thread](https://github.com/orgs/stellar/discussions/1923) before or during proposal submission.
* **Security**: tarball storage must be tamper-evident; rebuild environment isolated from host; submitted code must not exfiltrate secrets or affect other submissions; write endpoints must have abuse and DoS protections.
* **Audit**: third-party security audit required before production launch. Scope: rebuild environment, tarball integrity, API authentication, image allowlist policy. Auditor coordinated by SDF via the audit bank.
* **UX**: a contract developer should verify a deployed contract in under 15 minutes from reading the docs to seeing the verification appear.
* **Decentralization of verification**: architecture must allow multiple independent verifier instances to publish results. Proposals describe how disagreement surfaces and how consumers pick a trusted set.
* **Performance:** verification requests complete or return queued status within 5 minutes for standard contract sizes.
* **Availability:** public query API targets 99%+ uptime.
* **Storage and retention:** vendors propose tarball and rebuild-artifact retention policy. Egress cost ownership made explicit.
* **Operational ownership post-grant:** hosting, on-call rotation, and funding tail addressed in the proposal.
* **Compliance:** operable as a public good without KYC or gated access. No user data collection beyond what's necessary for abuse prevention.
* **Openness:** codebase open-source and self-hostable. Production deployment should allow community operation over time.<br>

**Interfaces SDF will provide before contract execution:**

* The CLI to Service interaction contract (being resolved internally). Vendors should support either a service-mediated submission flow or a decentralized on-chain result discovery model; SDF will name the shape before the design phase.
* The stellar-cli-docker image allowlist endpoint and trust criteria for adding image sources.
* Any SEP-58 amendments landing before the vendor's design phase (e.g., the home\_domain field amendment under discussion).

#### 4. Evaluation Criteria

* **Technical capability:** demonstrated experience building reproducible build pipelines and verification infrastructure. Familiarity with Sourcify, solana-verify, or equivalent is strong evidence.
* **SEP-58 alignment:** proposal maps to the SEP-58 vocabulary and consumes SDF-published trusted images via bldimg.
* **Display-layer design:** how downstream tools (explorers, Lab, wallets) consume verification status without running their own rebuilds, including multi-verifier divergence UX.
* **Decentralization design:** concrete architecture for running multiple independent verifier instances.
* **Image trust policy:** allowlist policy and handling of image source eviction.
* **Relevant experience:** prior work on Sourcify or equivalent services, or deep Soroban / Rust toolchain experience.
* **Security & audit history:** track record of shipping audited infrastructure; threat modeling in the proposal.
* **Ecosystem alignment:** willingness to coordinate with explorer teams (Stellar Expert, StellarChain), SDF tooling teams (stellar-cli, Stellar Lab), and ongoing SEP discussions ([SEP-58](https://github.com/orgs/stellar/discussions/1923), the forthcoming verifier-API SEP, SEP-55 evolution).
* **Ability to deliver within required timeline:** realistic milestone plan.
* **Coherent integration plan:** how explorers and other consumers adopt the service, including API stability guarantees and the path to conformance with the forthcoming verifier-API SEP.

#### 5. Expected Deliverables

* Verification service codebase, open-source and self-hostable.
* Public deployment for Mainnet and Testnet.
* Stable public API with documented schema and versioning policy.
* SDK or client library for querying verification status, designed to conform with the forthcoming verifier-API SEP once authored.
* Contract developer CLI or submission interface.
* Image allowlist policy documented, with a published mechanism for adding new image sources.
* Integration documentation for explorers and downstream tools.
* User documentation for contract developers, contributed to Stellar Developer Docs.
* Test suite covering verification logic, API, rebuild environment, and image-trust signals.
* Security audit report and resolved findings (through Audit Bank).
* Production-ready service with operational runbook, monitoring, and on-call coverage.
* At least one reference integration, ideally [Stellar Lab](https://github.com/stellar/laboratory) or a cooperating verifier (OrbitLens / Stellar Expert, Aha Labs / rgstry.xyz, or 57B).

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

* A transaction recording / observation layer that can ingest either (a) a real on-chain transaction by hash on Mainnet/Testnet or (b) a locally simulated transaction (e.g., from a Soroban simulation against a forked state). The layer must extract structured information about which contracts were invoked, which functions, with which arguments, and the resulting state changes / token movements.
* A context rule + policy synthesizer that converts the recorded transaction(s) into a proposed context rule (scope: which contracts and functions; lifetime: how long the permission lasts) plus the smallest set of policies needed to constrain the rule (e.g. spending limits derived from the observed amounts, frequency limits, time bounds). The synthesizer should bias toward minimal permissions -- if a transaction sequence only ever calls two functions with two specific assets, the generated rule should not permit a third.
* Generated policy code in Rust, suitable for compilation as a Soroban contract, leveraging existing OZ-provided policy primitives (simple\_threshold, weighted\_threshold, spending\_limit) wherever they suffice. The tool should compose existing policies first and only generate net-new policy contracts when the constraint cannot be expressed by combining standard ones. Where new policy code is generated, it must implement the Policy trait correctly, including proper storage segregation for stateful cases.
* An MCP server that exposes the recording, synthesis, and verification capabilities to agents, so that an AI agent can both request a policy be drafted from a sample transaction and operate under that policy once installed. The MCP interface should be agent-friendly: structured inputs/outputs, deterministic behavior, machine-readable error codes. Get inspiration from the [Cloudflare Agent Setup](https://developers.cloudflare.com/agent-setup/) and how they handle plugins, mcp and skills.
* An Agent skill (or equivalent for other agent frameworks) that wraps the MCP and gives an agent a high-level conversational entry point: "the user wants to grant permission to do X; here is a transaction they performed; draft a policy." The skill should know when to ask for clarification (e.g., "this transaction transferred 50 USDC -- should the policy cap at 50, or allow up to 100 over a week?"). Can be for Claude and similar tools.
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
Important: If you were referred by a member of the SCF community, make sure to include their unique referral code on this form.
{% endhint %}

2. Eligible teams will be invited to submit to an upcoming Build round. Submit your Build form before the deadline and choose the RFP Track. In the submission form, clearly identify which open RFP you’re addressing.
3. Submissions are reviewed by 2 reviewers from that quarter’s Category Delegate Panel.
4. If reviewers agree Yes or No, the project moves forward. If reviewers disagree, a third reviewer is added to break the tie. At this stage, teams may be asked to meet with reviewers to go over their submission in more depth.
5. Some teams may receive requested minor changes to their submission before funding.
6. After making any requested changes, awarded submissions receive their first tranche of funding.
7. Once funded, each subsequent tranche must be submitted within 90 days of the previous payment. Teams that miss a deadline without notifying the SCF team in advance forfeit the remainder of their award. See Tranches & Deliverables and the Official Rules for full details.
