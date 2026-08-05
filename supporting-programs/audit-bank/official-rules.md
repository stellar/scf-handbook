# Official Rules

Each participating project (“Project”, “project” or “Participant”) needs to meet the Participant Eligibility Rules, the Application and Evaluation criteria, as well as the General Rules (altogether known as “Official Rules”).&#x20;

## Structure

The Soroban Security Audit Program (the “Program”) is structured to enhance the safety and security of Soroban ecosystem projects. Managed by the Stellar Development Foundation (“SDF”), the Program schedules audits for projects and covers up to 100% of the audit cost (see details of [co-payment here](official-rules.md#phase-5-audit-execution-and-audit-fees)) with reputable audit firms and strategically allocates them to high-impact projects building on Stellar. Projects undergo a rigorous assessment and auditing process, ensuring robust security, mitigating risks, and fostering trust within the Stellar ecosystem.

### Approved Audit Firms

The following audit firms have been pre-approved by the Stellar Development Foundation to participate in the Soroban Security Audit Bank. Additional audit firms coming soon.

* [Certora](https://www.certora.com/): Specializes in Web3 security providing both audits and formal verification of smart contracts based on mathematical reasoning of code.
* [Code4rena](https://code4rena.com/): Code4rena is a competitive audit platform where 100+ top security researchers review your code per audit, uncovering high-severity bugs before deployment—so you can launch to Mainnet with confidence.
* [ChainSecurity](https://www.chainsecurity.com/): Founded in 2017, ChainSecurity is a leading smart contract auditing firm specializing in securing complex code that powers critical Web3 infrastructures.
* [Halborn](https://halborn.com/): Founded in 2019, Halborn provides world-class security assessments and consulting for Web3 and Fortune 500 clients—protecting against crypto-specific threats like smart contract exploits, social engineering, and infrastructure breaches.
* [Oak Security](https://oaksecurity.io/): Securing Web3 since 2017, Oak Security has completed over 600 audits without a single exploit. Oak Security’s signature ‘blinded’ process guarantees that every line of code is reviewed by multiple auditors in parallel. Fast, robust, secure.
* [OtterSec](https://osec.io/): Focused on identifying and patching critical exploits before protocols go to market; known for securing over $36,000,000,000 in total value locked (TVL) across 120+ protocols of major ecosystems.
* [Runtime Verification](https://runtimeverification.com/): Offers formal methods and runtime verification techniques to enhance blockchain system safety and reliability, starting with an in-depth design and specification review to ensure deep understanding of the protocol.
* [Spearbit + Cantina](https://cantina.xyz/welcome): Cantina and Spearbit combine a world-class security researcher network with purpose-built tools - delivering scalable and effective solutions pre-deployment through runtime all in one platform.
* [Veridise](https://veridise.com/): Offers rigorous smart contract and ZK circuit audits backed by deep blockchain security expertise and advanced in-house vulnerability detection tooling.
* [Zellic](https://www.zellic.io/): Zellic is a leading security research firm specializing in blockchain and cryptography, led by world-class white-hat professionals and trusted by top projects for uncompromising security.

### Program Phases

<table data-header-hidden><thead><tr><th width="149.75390625"></th><th width="386.73046875"></th><th></th></tr></thead><tbody><tr><td>Phase</td><td>Description</td><td>Duration</td></tr><tr><td>Intake &#x26; Eligibility</td><td>Projects submit audit requests based on clearly defined eligibility criteria.</td><td>-</td></tr><tr><td>Readiness Review</td><td>Each project undergoes a mandatory readiness assessment by a security expert, including threat modeling.</td><td>&#x3C;4 weeks</td></tr><tr><td>Audit Scheduling</td><td>Audits scheduled with pre-approved audit firms based on importance, ecosystem impact, availability, and readiness.</td><td>1 week</td></tr><tr><td>Pre-Audit Preparation</td><td>Participants are encouraged to perform self-administered code and security checks with recommended tooling.</td><td>2–3 weeks</td></tr><tr><td>Audit Execution</td><td>Audits conducted by pre-approved audit firms.</td><td>1–6 weeks</td></tr><tr><td>Post-Audit Resolution</td><td>Participants receive a private audit report detailing vulnerabilities and address these promptly.</td><td>1–4 weeks</td></tr><tr><td>Verification and Follow-Up</td><td>Security experts verify remediation; additional audits or formal verification for high-value projects.</td><td>2–3 weeks</td></tr></tbody></table>

#### **Phase 1: Intake & Eligibility Submission**

Projects interested in participating must submit an audit request using a provided intake form. This intake form is provided to SCF-funded projects which have reached Testnet stage or are already on Mainnet. This form will detail the division of audit costs between SDF and the projects, and will require detailed information about the project, including:

* Project description and purpose
* Smart contract and technical architecture details
* Development status and GitHub repositories
* Previous security practices or audits

Use the [Audit Readiness Checklist](audit-readiness-checklist.md) and make sure your submission meets all the criteria to pass Readiness Review.&#x20;

#### **Phase 2: Readiness Review**

Upon receiving the intake form, the project will undergo a thorough Readiness Assessment, including:

* Eligibility assessment
* Threat modeling to identify potential security risks
* Assessment of the completeness of provided documentation
* Codebase maturity and review of initial security measures implemented

This phase is expected to take anywhere from 1 to 4 weeks (depending on the back and forth needed), after which the project will be informed of its eligibility and readiness status.

#### **Phase 3: Audit Scheduling**

If a project passes the readiness review, it moves into audit scheduling. Multiple quotes from pre-approved audit firms will be gathered based on the project's scope and complexity. Audits are then scheduled based on SDF's discretion depending on the best fit considering:

* Expected scope
* Strategic ecosystem impact
* Project readiness
* Audit firm availability
* Project’s preference (if expressed in submission form)

Scheduling decisions are communicated clearly to the participating project.

#### **Phase 4: Pre-Audit Preparation**

Participants are expected to use self-service security tooling and internal testing to identify and fix vulnerabilities prior to the external audit. The project team should perform:

* Automated testing with recommended security tools
* Internal code reviews
* Initial remediation of obvious vulnerabilities

This pre-audit phase spans approximately two to three weeks and does not delay audit scheduling.

#### **Phase 5: Audit Execution and Audit Fees**

The chosen audit firm performs a comprehensive security audit of the project's smart contracts and related infrastructure. This phase involves:

* Manual code reviews and automated tooling
* Penetration testing and stress testing
* Identification of critical, high, medium, and low vulnerabilities

While SDF covers most of the audit costs, there are cases in which an upfront co-payment from a project to SDF is required. As an example, for the Initial Audit, a project is required to provide a co-payment of 5% of Initial Audit costs to SDF, payable prior to commencement of the audit. However, if a project successfully addresses all identified critical, high, and medium vulnerabilities within 20 business days (verified by SDF with the Audit Firm), this co-payment of the Initial Audit will be fully refunded. Subsequent audits also require co-payment by the project. [See details here](official-rules.md#audit-co-payment-system).&#x20;

The duration of the audit phase typically ranges between one to six weeks, depending on the complexity of the project.

#### **Phase 6: Post-Audit Resolution**

After an audit is complete, projects receive a private, detailed report outlining identified vulnerabilities. To qualify for the refund of the 5% co-pay required for the Initial Audit, projects must promptly address these issues within the stipulated timelines, ideally resolving critical, high, and medium vulnerabilities within 20 business days. The audit firm verifies remediation measures undertaken by the project.

#### **Phase 7: Public Disclosure of Audit Results**

Upon successful resolution and verification, the final audit report is published publicly by the audit firm. This provides transparency and assurance to the broader Soroban community regarding the security status of the project.

By participating, projects agree to all phases of this structure, committing to transparency, timely remediation of vulnerabilities, compliance with co-payment obligations, and maintaining the highest security standards to safeguard the Soroban ecosystem.

### Audit Co-Payment System

To ensure accountability and efficient resource allocation, projects may be required to co-pay for audits based on their TVL (Total Value Locked) or equivalent traction milestones:

<table><thead><tr><th>Audit Stage</th><th>Traction Threshold</th><th width="127.91796875">Co-Payment %</th><th width="258.55078125">Description</th></tr></thead><tbody><tr><td>Initial Audit</td><td>None for priority categories</td><td>5% with potential refund*</td><td>Covers initial audit to ensure baseline security for newly developed protocols.</td></tr><tr><td>Growth Audit</td><td>>$10,000,000 TVL or equivalent</td><td>0%</td><td>Focused on scaling projects with moderate traction to validate ongoing security. May include more extensive auditing (e.g. formal verification)</td></tr><tr><td>Scale Audit</td><td>>$100,000,000 TVL or equivalent</td><td>0%</td><td>Targets high-value projects nearing maturity to ensure robust security measures. May include more extensive auditing (e.g. formal verification)</td></tr><tr><td>Pre-Traction Follow Up Audits<br></td><td>N/A</td><td><p>20% for the pre-traction follow-up audit, 50% for the second pre-traction</p><p>follow-up audit</p></td><td>If additional audits are needed in addition to the Initial Audit and the project hasn’t achieved traction required for Growth and Scale Audit yet, SDF partly covers the first two follow-up audits. </td></tr></tbody></table>

\*If the project is able to successfully address all critical, high, and medium issues identified by the Audit Firm within 20 business days, the 5% co-payment of the Initial Audit will be refunded back to the project.&#x20;

## Participant Eligibility

In order to be eligible for an audit, projects must meet the following criteria:

* Projects must have been funded by SCF. Companies with other commercial grants from the SDF are not eligible for participation in the audit bank.
* Projects must pass KYC and sanction checks.
* Projects must be in an [eligible priority category or meet non-priority traction criteria](official-rules.md#eligible-categories).
* Projects must have completed the development of the code portions within the audit scope, be nearly Mainnet-ready, and require an audit within 4–6 weeks.&#x20;
* Projects must have conducted extensive tests on their code and deployed it on Testnet for validation.
* As part of their application, projects must submit the results of one of the “self-service tooling” options to include a list of all identified vulnerabilities and a remediation plan for fixing identified critical, high, and medium severity vulnerabilities prior to audit start.
* Projects must include a STRIDE threat model for the project as part of their application.&#x20;
* Projects must be able to be responsive during the entirety of the audit.
* Projects must be able to cover co-pay depending on their audit stage.

### Eligible Categories

Projects must demonstrate increased risk or the potential for a significant impact on the ecosystem.&#x20;

#### **Priority Categories:**

* **Financial Protocols**: Protocols managing on-chain value, as they are prime targets for malicious actors.
* **Widely Used Applications**: Applications using Stellar smart contracts that are expected to have large-scale adoption ($1,000,000+ TVL, 100K+ active users), where vulnerabilities could undermine user trust.
* **Infrastructure Contracts**: Oracles, vaults, account abstraction contracts, or similar components that are widely integrated across multiple services.
* Yield-Bearing Token Protocols: Protocols representing real-world value through smart contracts.

#### **Non-Priority Categories Criteria:**

Projects outside of priority categories must reach a threshold of 10K MAA, $100,000 in TVL or transaction volume to potentially qualify for an audit post-launch, but must obtain review panel approval first.&#x20;

#### **Eligibility Examples**

{% hint style="info" %}
Example 1: A financial protocol managing $500,000 TVL would qualify for an audit due to its high-risk nature and ability to significantly impact the ecosystem if compromised.
{% endhint %}

{% hint style="info" %}
Example 2: An escrow account project with <$100,000 TVL would qualify only after reaching the $100,000 TVL threshold for non-priority categories and receiving review panel approval based on a valid justification (e.g., without an audit, a breach or vulnerability in the project could have medium- or high-severity consequences and result in the loss of user funds).
{% endhint %}

### General Rules

#### 1) Publicity

By applying to the Soroban Security Audit Bank Program, Participants consent to the use of their personal information by the SDF and third parties acting on behalf of SDF. Such personal information includes Participant's name, likeness, photograph, opinions, comments, and hometown and country of residence ("Participant Profile"). Participant Profiles may be used for advertising and promotional purposes in the following channels: (a) the SDF website ([stellar.org](http://stellar.org) and its subdomains), (b) SDF's official social media accounts, (c) SDF blog and newsletter publications, (d) SDF conference and event presentations, and (e) the published audit report page at [stellar.org/audit-bank/projects](http://stellar.org/audit-bank/projects) (collectively, "Approved Channels"). Use of a Participant Profile in any channel other than the Approved Channels requires the Participant's prior written approval. Participant Profiles may be used for advertising and promotional purposes in the Approved Channels without further payment or consideration, and without right of review. The duration of this consent is for a period of three years following the time of audit completion of the last Soroban Security Audit payment, subject to a Participant's right of withdrawal under Section 4 below.\
\
SDF shall use a Participant's name, logo, and trademarks only in their original, unaltered form, only in the Approved Channels (or with the Participant's prior written approval for use outside the Approved Channels), and in accordance with any brand guidelines the Participant has provided to SDF in writing.\
\
Use of opinions or comments attributed to a named individual associated with a Participant requires that individual's prior written consent. This requirement does not apply to organizational-level references to the Participant's project name or participation status.\
\
This consent applies, as applicable, to all members of the Participant that has been selected for the Soroban Security Audit program.

#### 2) Disclaimers & Limitations of Liability

‍In addition to the disclaimers, limitation of liability, and indemnities agreed to in the main [SDF Terms of Service](https://stellar.org/terms-of-service), Participants also specifically agree to release and hold harmless SDF and its respective affiliates, employees, and agents from any and all liability or any injury, loss or damage of any kind arising from or in connection with SDF and its promotion, or any Awards granted in connection with SDF.

#### 3) General Conditions

SDF reserves the right, in their sole discretion, to cancel, suspend and/or modify the Soroban Security Audit Bank, or any part of the Official Rules for any reason.

The Soroban Security Audit Bank is governed by the [SDF Terms of Service](https://www.stellar.org/terms-of-service) and the Official Rules. If there is any conflict or inconsistency between the SDF Terms of Service and the Official Rules, the Official Rules will prevail. If there is any discrepancy or inconsistency between the terms and conditions of the Official Rules and disclosures or other statements contained in any Soroban Security Audit Bank materials, including but not limited to the Soroban Security Audit Bank Submission form, and/or the Stellar.org website, then the Official Rules shall prevail.

The terms and conditions of the Official Rules are subject to change at any time, including the rights or obligations of the Participants and SDF. SDF will post the terms and conditions of the amended Official Rules on the Stellar.org website. To the fullest extent permitted by law, any amendment will become effective at the time specified in the posting of the amended Official Rules or, if no time is specified, the time of posting.

SDF’s failure to enforce any term of the Official Rules shall not constitute a waiver of that provision. Should any provision of the Official Rules be or become illegal or unenforceable in any jurisdiction whose laws or regulations may apply to a Participant such illegality or unenforceability shall leave the remainder of the Official Rules, including the Rule affected, to the fullest extent permitted by law, unaffected and valid. The illegal or unenforceable provision shall be replaced by a valid and enforceable provision that comes closest and best reflects the SDF’s intention in a legal and enforceable manner with respect to the invalid or unenforceable provision.

#### 4) Data Privacy and Confidentiality

SDF collects personal information from Participants when they enter the Soroban Security Audit Bank. The information collected is subject to the privacy policy located here: [https://www.stellar.org/privacy-policy](https://www.stellar.org/privacy-policy)\
\
A Participant may withdraw consent to the processing of its personal information (including the use of Participant Profiles under Section 1) at any time by providing written notice to [sorobanaudits@stellar.org](mailto:sorobanaudits@stellar.org). Withdrawal is prospective only and does not affect the lawfulness of any processing that occurred, or materials that were published or distributed, before SDF's receipt of the withdrawal notice. Withdrawal of consent to the processing of personal information that is required for participation in the Program may result in the Participant's inability to continue in the Program.\
\
SDF may engage third-party service providers in the following categories to process personal information or Participant Profile data on SDF's behalf in connection with the Program: (a) identity verification and sanctions screening providers, (b) cloud infrastructure and hosting providers, (c) marketing and communications service providers, and (d) pre-approved audit firms as listed at [stellar.org/grants-and-funding/soroban-audit-bank](http://stellar.org/grants-and-funding/soroban-audit-bank). SDF will update this list of categories if it engages processors in a materially different category.\
\
Any and all code, documentation, or other proprietary materials ("Confidential Information") that Participants submit to SDF for the purposes of the Program will be protected by SDF. SDF will not use Participants' Confidential Information for any purpose other than to perform its readiness review and assign an audit firm for the audit. Access to Participants' Confidential Information will be restricted to SDF personnel who are directly involved in the Program.\
\
SDF's confidentiality obligations will not extend to any information that is (a) already publicly known, (b) independently developed by SDF without reference to a Participant's Confidential Information, (c) becomes known to SDF through disclosure by sources other than a Participant without such sources violating any confidentiality obligations to such Participant, or (d) required to be disclosed by law.\
\
Any audit will be conducted by an independent, third-party audit firm. SDF will notify the Participant of the identity of the audit firm assigned to the Participant's engagement before audit work begins. The current list of approved audit firms is published at [stellar.org/grants-and-funding/soroban-audit-bank](http://stellar.org/grants-and-funding/soroban-audit-bank). SDF retains sole discretion over audit firm assignment but will give good-faith consideration to any documented conflict of interest raised by the Participant before the engagement commences. While SDF will disclose Confidential Information to the selected audit firm for the sole purpose of conducting the audit, this audit firm is not an employee or agent of SDF. SDF is not responsible or liable for the actions, omissions, or any breach of confidentiality by such audit firm. SDF strongly recommends each Participant enter into a separate agreement covering confidentiality obligations directly with the audit firm who will be performing the audit.

#### 5) Contact

If you have any specific questions or concerns you can also email SDF at sorobanaudits@stellar.org.
