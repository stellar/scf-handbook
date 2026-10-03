# Integration Track

> [**Find the current Integration List here**](integration-list.md)

The Integration Track supports applications leveraging existing building blocks on Stellar to enable everyday financial services, creating a plug-and-play experience for builders submitting to the SCF.

Rather than reinventing the wheel, this track focuses on composability: integrating wallets, assets, on- and off-ramps, and DeFi protocols to create a more connected, user-ready ecosystem.

#### ✅ Who This Track Is For

* Teams that have applications with existing traction integrating with:
  * Stellar wallets
  * Anchors or on/off-ramps
  * DEXs and DeFi protocols
* Builders who want to combine ecosystem pieces, not build new ones.

#### 🚫 Who This Track Is Not For

*   Teams building net-new applications (including wallets) without existing traction

    → Better fit for [Instawards](../../instawards/)
* Teams building net new protocols not focused on integrations\
  → Better fit for the [Open Track](../open-track.md)
* Developers creating tools or libraries intended for other devs\
  → Check out the [RFP Track](../rfp-track.md)

***

#### Track Requirements

* You must integrate with at least one building block from the [official SCF Integration List](integration-list.md)
* Explain clearly:
  * What you’re integrating
  * How it improves your product and why it’s important to your success
  * Your existing user traction and how the Stellar integration would create value in the Stellar ecosystem
* Most of your budget should go towards your integration costs.
* Propose an onchain success metric for your final tranche. Your submission must include a measurable onchain threshold: a NAV (Network Asset Value) target, cumulative payment/transaction volume, or an equivalent onchain measure appropriate to your integration that your project commits to reaching for release of the final tranche (#3). You set the bar; the review panel ratifies or adjusts it during panel review. The point is to prove real usage, not to hit an aggressive growth target: a modest, credible number is fine.<br>

***

#### Budget Recommendations

Ensure you’re not overscoping your budget. Most integration partners on the list take less than a week (40 hours) of development time to integrate. Find more information about your chosen integration partner [here](https://airtable.com/appymB1sbp5uidiGe/shrQFLSRUqxI7tBdT).

<table><thead><tr><th width="122.6484375">Scope</th><th width="375.43359375">Example</th><th>Suggested Budget</th></tr></thead><tbody><tr><td>Small</td><td>one simple integration (wallet, SDP, MGI)</td><td>$25,000–$50,000</td></tr><tr><td>Medium</td><td>moderate scope: one larger integration (DeFi protocol) or two small ones</td><td>$50,000–$100,000</td></tr><tr><td>Large</td><td>complex integrations: Wallet + DeFi protocol + on-ramp, anchor + DEX, or cross-chain bridge deployment.</td><td>$100,000–$150,000</td></tr></tbody></table>

Feel free to use the above table as a guide for creating your budget. Your budget items should mainly be related to your integration costs, but some costs for “connective tissue” are permitted.

* Use the Budget Guidelines to format your ask
* Split into 3 tranches using SCF’s milestone model
* Do not include audit or marketing costs (except as expressly permitted below)

***

### Outcome-Based Final Tranche (Tranche #3)&#x20;

For Integration Track awards, the final tranche (#3, 40% of the award) releases when your project reaches its committed, panel-ratified onchain metric — not on mainnet launch alone. Tranches #0–#2 (10% on award acceptance / 20% MVP / 30% testnet) are unchanged, as is your total award size.

How it works:

* You propose a metric type (NAV, cumulative volume, or an equivalent onchain measure), threshold, measurement window and onchain footprint type in your submission .
* The panel ratifies or adjusts the proposal during panel review.
* At award time you register your onchain footprint — Soroban contract IDs, asset issuing accounts, app-operated wallets, and sponsored accounts (per CAP-33) — so activity is attributable to your product. A shared per-project dashboard keeps the threshold check transparent to you, the panel, and downstream programs.
* The threshold is measured over an agreed window, not a single-day snapshot. Upon review, the panel may disregard activity that is self-generated, wash, or otherwise clearly gamed.

#### User-Testing Budget Allowance

A portion of tranche #2 and tranche #3, capped at one-third (1/3) of the total budget, may be spent proving the flow with real initial users, e.g. user-testing events; provided that SDF/SCF retains the discretion to adjust such cap at any time. The one-third (1/3) cap is a ceiling, not an entitlement or guarantee: the actual budget allocated to these narrow and validation-focused user-testing activities must be narrowly tailored, concrete, and credible, and must be disclosed as a separate line item in the budget section of the application. This allowance is not intended for broad paid user acquisition.&#x20;

The guiding principle: funds should be used for activities that bring users to your product to learn what it is, how it works, whether it works, and how it can be improved - not for incentives, reward/award-for-action, challenges or volume-based campaigns to acquire large numbers of paid users. All acceptable uses below are subject to the content restrictions and unacceptable-usage restrictions that follow.

**✅  Acceptable Uses (subject to the content restrictions and unacceptable-usage restrictions further below):**

* Purely informational and educational content:
  * Technical blog content: explaining how the product works, who it is for, and why it matters.
  * Explainer video production: animated or live demo videos.
  * Translation / localization: expanding reach into non-English markets relevant to Stellar’s core use cases (e.g., remittance, emerging markets).
  * Landing page design: the conversion layer for other outreach.
* Limited community outreach and retention:
  * Email list infrastructure: CRM/newsletter tooling to build an owned audience.
  * Product validation activities: pilots, UX testing, early go-to-market strategy testing, early product-market-fit efforts, focus groups, user-testing panels, and similar.
* In-person demo events
  * Small hosted events where users try the product live. Budget covers logistics only, not user rewards.

**Unacceptable Uses**

* Any campaign where the user's motivation to engage is a financial incentive tied to on-chain behavior, including:
  * Referral rewards tied to on-chain actions
  * Token incentives for liquidity, volume, or deposits
  * “Trade-to-earn” / “deposit-to-earn” promotions
  * Market making or artificial volume generation
  * Any variable reward structure where payout scales with on-chain behavior
  * Any incentive, reward/award-for-action, challenge, or volume-based activity or campaign
* Paid distribution, business development, and earned-media spend, including:
  * Wallet / aggregator listings
  * Hackathon bounties (including sponsoring challenges that reward participants)
  * Press / earned-media outreach (PR firms or paid journalist placements)
* Other prohibited acquisition tactics: paid influencers, incentive campaigns, airdrops, pump-and-dump activity, volume generation, and similar.

**Content Restrictions**

Any content produced with SCF award funds must comply with the following:

* No financial framing. No award-funded content may reference yields, returns, investment opportunity, “earn,” “rewards,” price appreciation, or comparative financial performance.
* No endorsement claims. Content may not use “Backed by SDF,” “SDF-approved,” “official Stellar partner,” or any formulation suggesting endorsement, audit, representations and warranties by SDF or SCF.
* No SDF branding. No use of the SDF logo and no representations, express or implied, of SDF endorsement.
* Permitted attribution. The product may state that it is “built on Stellar” or a “recipient of an SCF award,” but must be accompanied by the disclaimer below\*.

**Required Disclaimer**&#x20;

Draft to accompany any permitted “built on Stellar” / “recipient of an SCF award” reference:

\*\[Product] is an independent project developed and operated by an independent developer. While \[Product] is built on Stellar and is a recipient of a Stellar Community Fund (SCF) award, it is not built, operated, endorsed, audited, reviewed, vetted, or guaranteed by the Stellar Development Foundation (SDF) or the SCF. The phrases “built on Stellar” and “recipient of an SCF award” refer only to the project’s use of Stellar's open-source technology and its receipt of award funding, and do not create or imply any partnership, affiliation, or endorsement. SDF and SCF make no representations or warranties regarding \[Product] and are not responsible for its performance, security, or compliance.

**Consequences of Breach**

Violation of any of the above may result in remedial action by SDF, as set out in Section 3(A)(f) of the [Official Rules](../../official-rules-for-submissions.md). These remedies are cumulative and in addition to SDF’s rights under the [Official Rules ](../../official-rules-for-submissions.md)and the SDF Terms of Service.

***

### Process & Timeline

1. Submit the SCF Interest form and indicate your interest in the Integration Track.

| Important: If you were referred by a member of the SCF community, make sure to include their unique referral code on this form. |
| ------------------------------------------------------------------------------------------------------------------------------- |

2. Eligible teams will be invited to submit to an upcoming Build round. Submit your Build form before the deadline and choose the Integration Track.<br>
3. Submissions are reviewed by 2 reviewers from that quarter’s Category Delegate Panel.<br>
4. If reviewers agree Yes or No, the project moves forward. If reviewers disagree, a third reviewer is added to break the tie. At this stage, teams may be asked to meet with reviewers to go over their submission in more depth. As part of this review, reviewers also ratify or adjust your proposed final-tranche onchain threshold, guarding against thresholds that are trivially low or unrealistically high.<br>
5. Some teams may receive requested minor changes to their submission before funding.<br>
6. After making any requested changes, awarded submissions receive their first tranche of funding.<br>
7. Once funded, each subsequent tranche must be submitted within 90 days of the previous payment. Teams that miss a deadline without notifying the SCF team in advance forfeit the remainder of their award. See Tranches & Deliverables and the Official Rules for full details.

***

#### Disclaimer Regarding Integration Solutions

The building blocks included in the SCF Integration List may include solutions developed by SDF as well as third-party solutions recommended based on feedback from the broader Stellar ecosystem. Inclusion on the list does not create any affiliation, partnership, or endorsement by SDF and does not constitute any representation or warranty by SDF regarding usability, intellectual property, compliance, technical requirements, or any other aspect of those solutions. Participants remain solely responsible for evaluating, selecting, and integrating these solutions into their projects, as appropriate.

Questions regarding any solution on the SCF Integration List should be directed to the company, the organization or the team maintaining that solution. SDF may assist in facilitating introductions or communications if requested, but is not responsible for support, performance, or compliance of any third-party solutions.
