# Audit Readiness Checklist

Incoming submissions are reviewed in detail and only those that can check all the below requirements, and don’t fall under any ineligible category, will be considered for selection. Also, make sure that your submission has all the context a reviewer may need and doesn’t require any additional context: the panel does not take any other information into account other than what is mentioned in the submission.

* [ ] **Funding**: Was the project funded through Stellar Community Fund and meet [eligibility requirements](official-rules.md#participant-eligibility)?
* [ ] **Repo Hygiene**: Does the structure of the code repository appear well organized and understandable?
* [ ] **Integration Tests**: Does the code repo include integration testing code? Have the integration tests been executed?
* [ ] **Threat Model**: Has a threat model been completed and provided or available? Does the threat model exhibit thought and assessment against the data flow diagram to sufficiently identify threats in the design? See [resource](https://developers.stellar.org/docs/build/security-docs/threat-modeling).
* [ ] **Dataflow Diagram**: Does the dataflow diagram appear to sufficiently explain the dataflow within the application? Does it properly identify trust boundaries and data entities? See [resource](https://developers.stellar.org/docs/build/security-docs/threat-modeling).

**Optional / Bonus:**

* [ ] **Tooling Scan**: Has the project provided a report from one of the [scanning tools](https://developers.stellar.org/docs/tools/developer-tools/security-tools) which operate well in the ecosystem?
* [ ] **Remediation plan**: Has the project provided a remediation plan for identified vulnerabilities from the [ecosystem scanning tool](https://developers.stellar.org/docs/tools/developer-tools/security-tools)?
