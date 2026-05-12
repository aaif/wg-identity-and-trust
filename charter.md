# Agentic AI Foundation Working Group Charter 
## Identity & Trust

### 1. Working Group Name
Working Group Name: Identity & Trust
Short Name / Acronym: [I&T]
Date Approved: [YYYY-MM-DD]
Last Updated: [YYYY-MM-DD]
Homepage / Repo (if applicable): [URL]
Primary Contact (Chair/Lead): [Grant Miller, grantd.miller@gmail.com]

### 2. Purpose and Mission

#### Mission Statement
The Identity & Trust Working Group advances the Agentic AI Foundation's mission by identifying and promoting vendor-neutral, interoperable standards and viewpoints for AI agent identity, attestation, authentication, delegation, and authorization—so agents can be discovered across platforms, prove who they are, who they act for, what they are allowed to do, and what human approvals occurred—enabling secure, privacy-preserving, and auditable agent interactions across systems and organizational boundaries. 

#### Why this Working Group exists (given the breadth of organizations represented can we identify approaches based on our collectively)
This Working Group was formed to address:

- How do we represent the identity of an AI Agent within an organization and trust identities shared between organizations?
- How do we represent agents who work on behalf of humans and/or execute processes?
- How do we authenticate agents and authorize their actions?
- How do we enable scalable adoption across global organizations while minimizing operational complexity and vendor lock-in?
- How do we ensure the solution is secure, auditable, observable, and interoperable with other working groups?

#### Alignment to Foundation Goals
The work of this WG supports:
- Supports methods for Identity to enable complex interactions within and across organizations, while maintaining the primary imperative that Agentic AI requires complex interaction. 
- Advance agentic AI technologies by advocating standards that establish trust by defining well understood and accepted Agent Identities. 

### 3. Scope

#### In Scope (what the WG will do)

**Agent Identity, Authentication, and Provenance**
 How an agent is identified, how it authenticates, and how it conveys where it came from, who operates it, and what software or system context produced it.

**Delegation and Authority Chains**
 How an agent represents that it is acting on behalf of a human, organization, role, team, service, or process; how those authorizations are delegated; and how far delegated authority extends.

**Authorization and Consent Models**
 How an agent conveys what it is allowed to do, for how long, under what policy constraints, and what human consent, approval, or governance controls apply, including support for the short-lived, fine-grained authorization patterns often required for agents.

**Trust Evaluation and Cross-Organizational Trust**
 How systems evaluate whether to trust an agent, including agents originating in another organization, and how to reason about whether the agent is authorized to take a requested action.

**Agent Discovery and Trust-Relevant Metadata**
 How agents are discovered and described, and what metadata is useful to support interoperability, trust establishment, observability, and traceability.

**Enterprise and Consumer Contexts**
 The Working Group considers both enterprise and consumer agent patterns, while remaining open to other deployment models that emerge over time.

#### Out of Scope (what the WG will not do)
- Develop or ratify formal standards on behalf of standards development organizations. The Working Group may inform, recommend, or contribute to standards efforts, but it is not itself a standards body.
- Define comprehensive agent security controls or secure execution architectures. Those topics are expected to be addressed primarily by other groups, especially Security and Privacy.
- Define ethical frameworks, public policy positions, or normative Responsible AI principles except where directly necessary to identity, consent, accountability, or trust representation.
- Build production-grade identity infrastructure or certification programs as a primary objective, though reference implementations or examples may be developed to validate guidance.

#### Assumptions and Dependencies
**Assumptions:** Other workgroups will define how to secure agents

**Dependencies:** This WG has dependencies or interactions with almost all the other WG's, but especially Security and Privacy, and Observability and Traceability.

### 4. Goals, Deliverables, and Success Criteria

#### 3-6-Month Goals 
- Define a taxonomy of common Identity terms used across organizations
- Understand the existing Agent Identity space including previously published positions from standards bodies and working groups.
- Identify, and address gaps in existing bodies of work

#### Planned Deliverables
For each deliverable, define owner, format, and target date.

- **Identity Taxonomy** — Owner: [Julianna Mealin], Format: report, Target: [2026-06-30]
- **Survey Landscape** — Owner: [Lin Sun - Wei Chen], Format: report, Target: [2026-06-30]
- **Identity Inventory** — Owner: [Role/Name], Format: report, Target: [2026-06-30]
- **Critical use cases** — Owner: [Monmohan, Wei, Lin, Yoshiyuki] Enterprise and consumer use cases
- **Identity Reference Architecture** — Owner: [Brian Malone, Monmohan Singh, Yoshiyuki Tabata], Format: report, Target: [2026-06-30]
- **Patterns**
- **Role of Discovery within Identity and Trust** [Wei/Jim/Junjie]

#### Definition of Done (DoD)
A deliverable is considered complete when:
- [Criteria #1, e.g., Deliverables reviewed/approved via WG process]
- [Criteria #2, e.g., Deliverables published in repo/site]

#### Success Metrics (KPIs) (pick a small set)
- **Community:** Active contributors, meeting attendance, issue throughput
- **Timeliness:** Deliverable targets and milestones met

### 5. Working Methods

#### Operating Model
- [Consensus-driven / chair-led consensus / voting as fallback]
- Work tracked in: [GitHub org/repo, issue tracker]
- Primary artifacts: [specs, reference implementations, guidance docs, test suites]

#### Meetings
- **Cadence:** [weekly]
- **Duration:** [60 minutes]
- **Time Zone Considerations:** [alternating times]
- **Open Meetings:** [Yes/No] (default: Yes)
- **Minutes/Notes:** [where notes are stored]
- **Recordings:** [policy and storage location, if any]

#### Communication Channels
- **Async:** [mailing list/Discord/Slack]
- **Sync:** [Zoom]
- **Announcements:** [mailing list/tag]

### 6. Membership and Participation

#### Who can participate
Participation is open to all individuals and organizations consistent with foundation policies.

#### Member Roles (customize as needed)
- **Participants:** anyone attending meetings or contributing asynchronously.
- **Contributors:** individuals making substantive contributions (issues, PRs, docs, reviews).
- **Maintainers/Approvers (optional):** individuals with approval rights in repositories.
- **Chairs/Co-Chairs:** individuals responsible for operations and facilitation.

#### Joining
To join, a participant should: Join mailing list + sign CLA/DCO if required.

#### Expectations
- Follow the Code of Conduct and collaboration norms.
- Make contributions in the open (issues/PRs) whenever possible.
- Declare conflicts of interest when relevant.

### 7. Governance and Decision-Making

#### Leadership Structure
- **Chair(s):** [Grant Miller]
- **Co-Chair(s):** [Alper Dedeoglu]
- **Secretary/Program Manager (optional):** [Name(s)]

#### Selection and Term
- Chairs are selected by: Election
- Term Length: 12 months
- Renewal: Allowed
- Removal/Resignation: [process]

#### Decision Process
- **Default method:** rough consensus documented in issues/meeting notes.
- **When consensus cannot be reached:**
  - Escalation path: [e.g., TC / Foundation Governing Board]
  - Fallback vote rules (if used): quorum [%], threshold [simple majority/supermajority], voting eligibility [contributors/maintainers].

#### Quorum (if voting is used)
Quorum is met when 50% eligible voters are present or 50% have responded asynchronously.

### 8. Relationship to Other Groups

#### Internal Coordination  
TBD

- **Liaison(s) to other WGs:** [Names/roles]
- **x/dependencies:** [list]

### 9. Intellectual Property, Licensing, and Compliance
(Use language consistent with foundation policies; customize only if you have explicit approval.)

#### Licensing
- **Code contributions:** [e.g., Apache-2.0/MIT] (or "per repository license")
- **Documentation/specs:** [e.g., CC-BY-4.0] (or "per repository license")

#### Contribution Requirements
Contributions must comply with: [DCO/CLA policy], repository contribution guidelines, and review requirements.

#### Antitrust and Competition Law
- Meetings and communications must follow the foundation's antitrust guidelines.
- Avoid discussions of pricing, market allocation, or other restricted topics.

#### Code of Conduct
This WG adheres to the Linux Foundation Project's Code of Conduct.

### 10. Security, Safety, and Responsible AI (Agentic AI-Specific)

#### Security Practices
- **Threat modeling expectations:** [required/optional]
- **Vulnerability disclosure process:** [link or description]
- **Security review gates for releases:** [e.g., dependency scanning, SAST, SBOM]

#### Agentic Safety and Risk Management
- **Safety considerations relevant to this WG:** [e.g., tool access control, prompt injection defenses, autonomy bounds]
- **Required practices (if any):** [e.g., evaluation harnesses, red teaming, abuse case documentation]
- **Data handling expectations:** [e.g., avoid sensitive data in issues/logs]

#### Privacy
- **Guidance for handling personal data:** [policy link/summary]
- **Logging/telemetry guidelines:** [what is acceptable]

### 11. Deliverable Lifecycle and Publication

#### Release Cadence
- **Expected cadence:** [quarterly/biannual/annual/as needed]
- **Versioning scheme:** [SemVer/date-based/spec versioning]

#### Review and Approval
- **Required reviewers:** [roles]
- **Approval mechanism:** [LGTM count, maintainer approval, chair sign-off]

#### Archival / Deprecation
- **Deprecation policy:** [how and when]
- **Sunset criteria:** [e.g., no activity for N months, goals achieved]

### 13. Amendments
This charter may be amended by:
[consensus/vote] of the Working Group, with [notice period] and documentation in [repo/location], and subject to [TOC/board] approval if required.

### 14. Ratification
By approving this charter, the Working Group commits to operating transparently, in the open, and in alignment with foundation policies.

- **Approved By:** [TOC / Governing Board / Steering Committee]
- **Date:** [YYYY-MM-DD]
- **Signatories (optional):** [Names/Titles]

## Optional Appendix A: Role Descriptions

### Chair
Runs meetings, sets agendas, ensures notes, drives milestones, represents WG in cross-WG coordination.

### Maintainer/Approver
Responsible for repository health, reviews/merges, release readiness, and technical direction.

### Contributor
Provides substantive work items (PRs/docs/issues), participates in reviews and discussions.
