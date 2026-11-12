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

RFPs are sourced from ideas submitted by the Stellar ecosystem, selected by Delegates through the [SCF Quarterly Process](quarterly-governance-process.md), and published here at the start of each quarter:

<details>

<summary><strong>Web and API Analytics for Stellar Ecosystem Projects</strong></summary>

### **Web and API Analytics for Stellar Ecosystem Projects**

### 1. Scope of Work

Design, implement, operate, and prepare for community handover a multi-tenant web and API analytics platform that the Stellar Community Fund (SCF) will run as a shared service for projects building on Stellar.

The platform must:

* Provide privacy-first, GDPR-compliant web analytics collected exclusively from frontend instrumentation.
* Ingest dual-exported OpenTelemetry data from tenant applications, discard heavy APM payloads (traces, spans, and deep logs), and convert the remaining data into standardized metrics stored in PostgreSQL.
* Enforce strict tenant isolation while giving designated SCF operators a global view.
* Support self-service enrollment of any project built on Stellar, with the ability for SCF operators to remove non-ecosystem projects and, if desired later, switch to an approval-required model.
* Be built upon either Umami or GoatCounter (proposer chooses one and justifies the choice).
* Ship as a fully open-source monorepo that includes all infrastructure-as-code, documentation, and operational artifacts needed for a community-appointed operator to assume stewardship.

The proposer is responsible for 12 months of hosting and support after the final development tranche is approved. During that window the system must be prepared for orderly handover of stewardship.

### 2. Background & Context

SCF currently lacks a unified, trusted source of end-user usage data for the projects it funds. Reviewers therefore rely heavily on self-reported metrics, which creates unnecessary discussion, reporting overhead, and uncertainty when evaluating eligibility for follow-on programs such as Growth Hack, Public Goods Award, or traction requirements in the Integration Track.

At the same time, ecosystem visibility tools can answer “which projects claim to build on Stellar?” but cannot yet answer “which of those projects are actually being used?”

A shared analytics service solves both problems. Builders receive a reliable, low-friction, compliant analytics solution whose data is trusted by SCF. SCF operators obtain standardized dashboards that support fair comparisons and funding decisions. The broader ecosystem gains clearer signals of real usage.

For builders this means less time spent assembling and defending usage reports, faster and more predictable access to follow-on support programs, and stronger public visibility of real adoption — turning the analytics they already need into a shared asset that works for them rather than an extra reporting burden.

### 3. Requirements

#### 3.1 General

* Multi-tenant by design. Independent teams register sites/properties/APIs.
* Strict isolation: each tenant sees only its own data; designated SCF operators hold credentials for the global view.
* Self-service enrollment open to any project built on Stellar. SCF operators must be able to remove projects that are not part of the ecosystem. The system must support a later transition to an approval-required enrollment model.
* All application and infrastructure code must be released under an OSI-approved open-source license.
* The entire solution (including infrastructure-as-code) must live in a single open-source monorepo.
* Charges zero fees to tenants, SCF, or any other party.
* SCF operators must be able to generate and revoke API keys that grant access to metrics, intended for downstream machine consumers.
* Unknown-to-SCF builders are not eligible to respond to this RFP.

#### 3.2 Web Analytics

* Events must originate only from frontend code. The proposal must include a concrete strategy for detecting/mitigating bot traffic and artificial metric inflation (at minimum: distinguish real browser JS execution from pure server-side posts, and treat multiple distinct fingerprints from the same IP with skepticism). Build on the base project’s existing bot detection.
* Integration must be low-friction for a wide variety of sites (static HTML, SPAs, SSR frameworks).
* The script or snippet that tenants include must be pinned to a specific version. Dynamic remote updates of the tracking code are not permitted. Tenants must intentionally upgrade.
* Robust defense against supply-chain attacks is required; the proposer must describe its strategy.
* Minimum required metrics:
* Page views
* Unique visitors (privacy-first limitations on unique-visitor tracking across sessions are acceptable)
* Referrers
* Session duration
* Bounce rate
* Geographic distribution at country level
* Device and browser breakdown
* Custom events are a nice-to-have. Automatic capture of events from the Stellar Wallets Kit without tenant-side configuration is also a nice-to-have and left to the proposer’s discretion.
* Name the tracker script and API endpoints such that they do not trigger popular ad blockers.
* The solution must be GDPR-compliant without requiring client-side opt-ins. The proposer must:
* State any jurisdictions in which the solution would not be compliant without end-user opt-in.
* Explicitly declare data-residency choices.
* Design the system to minimize the set of users who can exercise right-to-erasure. If any personal data subject to erasure is stored, a practical tenant-triggered erasure workflow must be provided.
* Document the full privacy and compliance strategy (example approaches such as dropping the last octet of IP addresses before geolocation are acceptable).
* Tenant analytics dashboard: each enrolled project must have a private view that displays its own page views, unique visitors, referrers, session duration, bounce rate, country-level geography, and device/browser breakdown for selectable time ranges, with no access to any other tenant’s data.
* Global analytics dashboard: designated SCF operators must have a unified view that aggregates and compares the same core metrics across all enrolled projects, supporting filtering, sorting, and side-by-side comparison for funding and ecosystem-visibility decisions.

#### 3.3 API Analytics

* Tenants configure their applications to dual-export standard OpenTelemetry data to both their own APM backends and the SCF collector endpoint.
* Upon receipt the SCF collector must drop traces, spans, and deep logs, retaining only the information needed to produce standardized metrics (counters and histograms) that are written to PostgreSQL.
* Minimum required metrics / attributes:
* tenant.id / service.name — attribution to the correct project
* Normalized path / http.route — endpoint usage with variables removed
* http.response.status\_code — success vs. error rates
* Latency (http.client.duration or equivalent) — performance measurement
* Path normalization must be performed by a hard-coded default rule set that covers common patterns (numeric IDs, Stellar G-/C-/M-addresses, UUIDs, hex/crypto hashes, trailing slashes, etc.). No authenticated UI or API for tenants to add custom rules is required; tenants are expected to set the http.route attribute in their own middleware when finer control is needed.
* Design target: approximately 1 000 000 requests per day across all tenants.
* Aggregated views must be retained for at least 24 months (preferably longer). Raw metrics retention is left to the proposer for operational troubleshooting.
* Isolation rules are identical to the web path: tenants see only their own data; SCF operators see the global view.
* Tenant analytics dashboard: each enrolled project must have a private view of its own normalized endpoint traffic showing request volume, status-code distribution, and latency percentiles (at minimum p50/p95) for selectable time ranges, isolated from all other tenants.
* Global analytics dashboard: designated SCF operators must have a unified view that aggregates and compares the same API metrics across all enrolled projects, enabling identification of high- or low-usage services and fair cross-project evaluation.

#### 3.4 Hosting, Support & Handover

* The 12-month service window begins when the final development tranche is approved by SCF reviewers.
* The proposer must host the system and provide user support for the full 12 months.
* Expected operational targets (proposers compete on the concrete commitments they can make):
* Ingestion availability: 99.99 %
* Dashboard availability: 99.90 %
* Critical and high security vulnerabilities patched within 24 hours
* Support tickets responded to within 5 business days and fully resolved within 10 business days
* No mandatory on-call rotation or public support channel. A public issue tracker (GitHub or equivalent) is sufficient.
* Stewardship handover is expected to occur between month 6 and month 12 at SCF’s discretion. After 12 months the original proposer has no further obligations.
* Handover is complete only when a community-appointed operator is independently running a fully working system. Mandatory elements include transfer of repository ownership, full data migration, and either transfer of domain ownership or a permanent redirect from the old domain. Infrastructure can be rebuilt from the open-source monorepo.

### 4. Evaluation Criteria

Proposals will be evaluated on:

* Technical capability and soundness of the overall design
* Rationale of the choice for Umami or GoatCounter
* Relevant prior experience, especially open-source maintainer track record and multi-year history of work with SCF and/or SDF
* Strength of the privacy-first and security posture
* Quality of multi-tenant isolation and access-control design
* Realism and clarity of the proposed SLA and support model
* Clarity and completeness of the handover plan
* Coherent integration and onboarding plan for real SCF projects
* Quality of the open-source monorepo structure and documentation

Extra weight will be given to demonstrated open-source maintainer track record, privacy-first and security track record, and a history of working with SCF/SDF for multiple years. A weak track record may be disqualifying. Unknown-to-SCF builders are excluded.

### 5. Expected Deliverables

* Fully functional multi-tenant web + API analytics platform meeting all requirements above
* Complete open-source monorepo containing:
* All application code
* Full infrastructure-as-code
* Deployment documentation
* Operator runbooks
* Tenant onboarding guide
* Automated test suite
* Security and privacy/compliance documentation
* Monitoring and alerting baseline
* Live proof of adoption: at least three real SCF-awarded projects instrumented for web analytics and one project instrumented for API traffic, with both the live global operator view and a tenant-perspective screen-capture video demonstrating the experience
* Explicit statements on data residency, jurisdictions of GDPR compliance without opt-in, and the right-to-erasure workflow (if any personal data is stored)

### 6. Budget & Funding Structure (for internal review purposes only)

* Expected range: $40 000 to $60 000
* Payment structure: milestone-based tranches (10/20/30/40; final tranche must already demonstrate handover readiness)
* The 12-month service window starts only after the final development tranche has been approved by SCF reviewers
* SCF does not operate a formal SLA-enforcement process; selection therefore places significant weight on the proposer’s reputation within the Stellar ecosystem

</details>

<details>

<summary><strong>XDR/CAP-Coverage Audit Tool and Indexer-Hardening Guide</strong></summary>

### **XDR/CAP-Coverage Audit Tool and Indexer-Hardening Guide**

### 1. Scope of Work

This RFP seeks a team to build a shared test kit for applications that read the Stellar ledger: a library of rare but valid ledger data, a harness that replays it against an indexer and reports what breaks, a linter, and a guide for indexer authors. The same corpus doubles as a conformance suite for the Stellar SDKs that decode the ledger, so a bug fixed in one SDK becomes a regression test for all of them.

Deliverables:

* Tooling: a corpus of rare ledger and transaction patterns, one entry per pattern, tagged with the CAP that introduced it; a generator that produces them; and a replay harness that runs the corpus against any indexer and reports the shapes it mishandles or silently drops.
* Tooling: a conformance runner that replays the same corpus through at least the JavaScript, Go and Rust SDKs and reports where their decoding or encoding diverges from the network and from each other.
* Tooling: a linter, scoped to one language and framework that flags the three ingestion mistakes listed in section 3.
* Documentation: an indexer-hardening guide that explains which transaction fields stellar-core validates and which it does not, recommends depth and size caps, and shows how to handle muxed and signed-payload addresses.
* Integration: the corpus run against at least one SDF pipeline (wallet-backend or stellar-etl), with each failure triaged (severity, affected CAP, minimal reproducing entry) and filed upstream. The findings are the deliverable, not the run.

Deliverable specifications (inputs, outputs, reviewer check):

* Corpus and generator. In: CAP list, network history or a local stellar-core. Out: XDR files plus a manifest (entry ID, CAP, protocol version, source, synthetic flag, expected decoded values). Check: entries round-trip through rs-stellar-xdr and agree with --check-lcm goldens.
* Replay harness. In: corpus plus an adapter. Out: per-entry pass / mishandled / dropped report. Check: reference adapter reproduces wallet-backend#729, #731 and #716 on pre-fix commits and passes on the fixed ones.
* Linter. In: indexer source. Out: findings with rule IDs for the three mistakes in section 3. Check: flags seeded violations, runs clean on current wallet-backend.
* Guide. Out: fixed outline (validated vs. unvalidated fields, caps, participants-from-meta, muxed and signed-payload handling, checklist). Check: the field-by-field table agrees with the corpus manifest; publication is gated on review by a core or platform engineer.
* Conformance runner. In: corpus. Out: divergence matrix across the JS, Go and Rust SDKs. Check: reproduces js-stellar-sdk#1766, #1785 and #1789 on pre-fix tags.
* Findings reports. Out: one entry per finding (issue link, corpus entry, severity, component affected). Check: every failure maps to a filed issue.

### 2. Background & Context

Every application that reads the Stellar ledger has to decode XDR. Rare transaction shapes keep crashing those readers because nobody tested them, and each team rediscovers the same bugs on its own. A shape is a structural variant of a transaction, operation, or ledger entry: for example, a signer of the signed-payload type, or a trustline created by a contract call instead of by an account.

Two rules run through this RFP. First, stellar-core validates some fields of a transaction (signatures, sequence numbers, fees, time bounds) and passes others through untouched (memos, Soroban authorization trees, muxed account IDs). An indexer that trusts an unvalidated field can be crashed or fed bad data by anyone who submits a transaction. Second, an indexer should work out who a transaction affected from the ledger meta, which records what core actually changed, not from the transaction envelope, which records what the submitter claimed.

The evidence is recent. Wallet-backend ingestion was halted by bugs in three rare patterns: signed-payload signers (CAP-0040), unbounded authorization trees, and trustlines created by the Stellar Asset Contract that produce no trustline state change (CAP-0073). stellar-etl opened a Protocol 28 epic over roughly fifty correctness issues, including wrong effect types, lossy amounts, and fabricated muxed destinations. wallet-backend found muxed and signed-payload addresses being truncated. No shared corpus or replay harness exists, and no guide says which fields are safe to trust.

The same gap exists one layer down, in the SDKs that decode the ledger. A fix made in one Stellar SDK is not carried across to the others, so builders meet the same bug again in the next language. In September the JavaScript SDK rejected a valid liquidity-pool trustline operation because it ordered asset issuers by their string form instead of their XDR bytes. The Go SDK had hit and fixed that exact bug after a security report, and nobody had swept it across. An external node operator found it by ingesting testnet, not a test. An audit of the JavaScript SDK then produced fourteen decode and validation defects in two weeks, among them muxed account and offer IDs that decode to a different ID than they encode, map entries silently dropped when their keys collide, and union discriminants that accept floats. Every one was fixed in JavaScript alone; nothing checked whether the Go, Rust, Python or Java SDKs share the defect. A corpus of awkward but valid XDR with expected decoded values, run in each SDK’s CI, turns one team’s fix into every SDK’s regression test.

### 3. Requirements

**Functional Requirements:**

* The corpus covers the rare patterns introduced or changed by each CAP, tags every entry with CAP number and protocol version, and can grow as new CAPs ship.
* Corpus entries are XDR that stellar-core would actually emit, not just XDR that decodes. Entries are captured from testnet or mainnet history or produced by a local stellar-core; hand-crafted entries are marked synthetic in the manifest. Generation is reproducible for both testnet and mainnet passphrases.
* The replay harness feeds the corpus into a target indexer through a documented adapter interface and reports every shape the indexer mishandles or silently drops. It delivers ledgers through an input existing pipelines already consume, such as the Galexie data lake layout or a mock RPC getLedgers endpoint; proposals should say which one they will support first.
* The linter checks indexer source, in the agreed language, for three mistakes: trusting unvalidated fields, missing depth and size caps on recursive structures such as authorization trees and nested ScVals, and deriving participants from the envelope instead of the meta. The guide carries the same checks as a checklist for indexers in other languages.
* The guide covers, field by field, which transaction fields core validates; recommended caps; the participants-from-meta rule; and correct handling of muxed and signed-payload addresses, including the SEP-0023 strkey forms.
* The corpus is language-neutral: XDR files plus a manifest any pipeline can read. The generator may build on the Rust or Go XDR libraries. Where stellar-core publishes golden LedgerCloseMeta for its own CI (the --check-lcm mode), the corpus should agree with it.
* Each corpus entry carries its expected decoded values, so an SDK can check both that it decodes the entry and that re-encoding it reproduces the original bytes. The corpus includes the shapes that have already tripped one SDK but not the others: asset pairs whose issuers sort differently by strkey and by XDR bytes, muxed source and recipient accounts, muxed account and offer IDs that decode to a different ID than they encode, vectors at their maximum length, nested authorization entries, and maps whose keys collide after conversion.
* A conformance runner executes the corpus through at least the JavaScript, Go and Rust SDKs in CI, reports every entry where an SDK diverges from the network or from the other SDKs, and files a sibling issue in each affected SDK when a defect is found in one.

**Non-functional Requirements:**

* The generator and harness run offline, need no mainnet keys or funds, and are fast enough to run in CI on every pull request.
* The harness handles a full corpus without unbounded memory growth, since that is one of the failures it tests for.
* Open source under a permissive license, developed in public with regular status updates to the community.
* Built against the most recent stable release of the Stellar tech stack, with a plan for keeping up with protocol upgrades.
* A documented post-launch maintenance plan covering who maintains the deliverables and for how long.
* Clear documentation of the infrastructure the deliverables run on and of any user tracking, which should be minimal.

### 4. Evaluation Criteria

* Technical capability: depth of the proposed design and evidence that the team has shipped comparable developer tooling.
* Relevant experience: examples of past developer-focused work, with open-source repositories where possible.
* Security and audit history: prior security practices, audits, or disclosure handling on earlier work.
* Ecosystem alignment: the proposal responds directly to the needs in this RFP, and limits to scope are explained.
* Ability to deliver within the required timeline, with clear, testable milestones.
* Coherent integration plan: how the deliverables fit into existing Stellar tooling and how they will be maintained after launch.
* Open-source licensing and a commitment to building in the open, with regular public status updates.
* Demonstrated familiarity with Stellar XDR, CAPs, LedgerCloseMeta, and at least one ingestion pipeline (Horizon, stellar-etl, wallet-backend, or a third-party indexer).
* Reviewability: the proposal includes a draft manifest schema, two or three sample corpus entries, and evidence of reproducing one sighting from section 7. Proposals without these are incomplete.

### 5. Expected Deliverables

* Corpus and generator repository with a per-CAP coverage manifest.
* Replay harness with a documented adapter interface and one reference adapter.
* Linter for the agreed language, plus the checklist in the guide.
* Indexer-hardening guide, ready to publish on developers.stellar.org.
* Test suite and CI configuration for all tooling.
* Findings report from running the corpus against at least one SDF pipeline, with every finding filed upstream.
* Conformance runner for at least three SDKs, with a findings report of where they diverge and sibling issues filed in each affected SDK.
* Production release and a maintenance plan covering the first protocol upgrade after delivery.

### 6. Budget & Funding Structure (for internal review purposes only)

* Range: $50K to $75K, with $65K as the working estimate. The closest launched comparable is the State Optimization CLI ($70K), also analysis tooling with a validation requirement; treat it as a ceiling, not an anchor. The corpus is the cost driver: entries must be real core-emitted XDR across every CAP, reproducible on both passphrases, and consistent with stellar-core's golden LedgerCloseMeta.
* Milestone breakdown: (1) $25K: indexer-hardening guide, plus corpus and generator with per-CAP coverage manifest; (2) $25K: replay harness, documented adapter interface, one reference adapter (Galexie layout or mock getLedgers), the SDK conformance runner, and findings reports against an SDF pipeline and the three SDKs with issues filed upstream; (3) $7.5K: linter and self-audit checklist; (4) $7.5K: production release with Protocol 30 coverage, CI, and maintenance plan through the first protocol upgrade. If the linter is cut and the guide's checklist stands in for it, the total falls to about $57.5K.
* The SDK conformance runner (added 2026-11-02 from Airtable OPP-101) is absorbed into milestone 2 with no change to the total; its acceptance test is the reproduction of the three js-stellar-sdk issues listed in section 1.
* Payment on deliverables: funding is released in tranches on acceptance of each milestone, where acceptance means the section 1 checks for that milestone's deliverables pass. Each subsequent tranche must be submitted within 90 days of the previous payment, per the SCF Build Award rules.

### 7. Supporting Signals

These sightings are the evidence behind this RFP. Applicants can read the public items; they describe the failures this work should fix.

Public sightings:

* 2026-09-03: [stellar-core#5435 — add --check-lcm mode to verify golden LedgerCloseMeta in CI](https://github.com/stellar/stellar-core/pull/5435)
* 2026-09-04: [wallet-backend#731 — SAC-created trustlines produce no trustline state change (CAP-0073)](https://github.com/stellar/wallet-backend/issues/731)
* 2026-09-04: [wallet-backend#729 — handle CAP-40 signed-payload signers in ingestion](https://github.com/stellar/wallet-backend/pull/729)
* 2026-09-05: [henyey#3941 (experimental Rust rewrite of stellar-core) — validator dies during catchup on bucket-entry XDR parse failure, daily](https://github.com/stellar-experimental/henyey/issues/3941)
* 2026-09-10: [rs-stellar-xdr#581 — limit capacity reserved when decoding VecM](https://github.com/stellar/rs-stellar-xdr/pull/581)
* 2026-09-11: [stellar-etl#454 — \~50 data-quality issues opened in one audit sweep](https://github.com/stellar/stellar-etl/issues/454)
* 2026-09-15: [stellar-etl#470 — Protocol 28 Data Team epic opened over the ETL correctness backlog](https://github.com/stellar/stellar-etl/issues/470)
* 2026-09-18: [wallet-backend#716 — AddressBytea truncates muxed and signed-payload addresses](https://github.com/stellar/wallet-backend/issues/716)
* 2026-09-18: [stellar-etl#460 — P23+ event and effect gaps traced to an old SDK pin (CAP-0073)](https://github.com/stellar/stellar-etl/issues/460)
* 2026-09-25: [wallet-backend#753 — four indexer fixes closing findings from an ingestion-halt audit](https://github.com/stellar/wallet-backend/pull/753)
* 2026-09-28: [rs-soroban-sdk#2099 — MuxedAddress panics on a non-address ScVal](https://github.com/stellar/rs-soroban-sdk/pull/2099)
* 2026-09-29: [rs-stellar-xdr#598 — enforce VecM max length on serde deserialize](https://github.com/stellar/rs-stellar-xdr/pull/598)
* 2026-09-30: [js-stellar-sdk#1766 — order asset issuers and ScVal map keys like the network; the Go SDK had already fixed the same bug](https://github.com/stellar/js-stellar-sdk/pull/1766)
* 2026-10-06: [rs-stellar-xdr#604 — xdr-json schemas omit types and variants behind XDR feature flags](https://github.com/stellar/rs-stellar-xdr/issues/604)
* 2026-10-07: [js-stellar-sdk#1789 — scValToNative silently drops map entries whose keys collide](https://github.com/stellar/js-stellar-sdk/issues/1789)
* 2026-10-08: [js-stellar-sdk#1785 — muxed account and offer IDs accept values that encode a different ID](https://github.com/stellar/js-stellar-sdk/issues/1785)
* 2026-10-16: [js-xdr#165 — nine XDR validation issues opened and fixed in one audit pass](https://github.com/stellar/js-xdr/issues/165)
* 2026-10-16: [js-stellar-sdk#1823 — XDR string arms mangle non-UTF-8 bytes and lone surrogates](https://github.com/stellar/js-stellar-sdk/issues/1823)

</details>

If you have an need for a tool or infrastructure that would meet an immediate ecosystem need but isn't listed above, it could be a good idea for an SCF RFP—add it on the [Stellarlight Ideas page](https://stellarlight.xyz/) and discuss further in the [Stellar Dev Discord](https://discord.gg/stellardev)!

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
