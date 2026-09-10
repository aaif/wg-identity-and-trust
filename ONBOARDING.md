# Identity & Trust Working Group Onboarding

Welcome to the Agentic AI Foundation (AAIF) Identity & Trust Working Group (I&T). This guide explains what the group works on, how the breakout groups fit together, and the quickest ways to participate.

## Why this working group exists

Identity systems were largely designed for humans signing in to applications or workloads authenticating to other workloads. Agentic systems add new questions:

- Who or what is this agent, and where did it come from?
- Who authorized it, what authority was delegated, and how far may that authority flow?
- How should identity and delegation context survive agent-to-agent and cross-organization interactions?
- What evidence shows that a human approved a consequential action?
- How can a relying party discover an agent, evaluate trust, and audit what happened?

The working group develops vendor-neutral, interoperable viewpoints and guidance for agent identity, attestation, authentication, delegation, authorization, discovery, consent, and trust. See the [Working Group Charter](charter.md) for the formal mission and scope.

## Start here

1. Join the public [AAIF Discord server](https://discord.com/invite/9zTwngHAMy) and the [I&T Discord channel](https://discord.com/channels/1461090924791595243/1463637083737296979).
2. Join the public [mailing list](https://lists.aaif.io/g/wg-identity-trust).
3. Review the [running meeting notes](https://docs.google.com/document/d/1JfVIQBbxpMT28poaEyAwnINXRC9ZuLPg5q08G6CjPCM/edit?usp=sharing) and the [outstanding agenda](AGENDA.md).
4. Attend a Thursday meeting. The group alternates between 6:30 AM and 9:00 AM Pacific Time; use the links and calendar in the [README](README.md#meetings).
5. Choose a breakout group or an open agenda item and introduce yourself in Discord or at a meeting.

Participation is open to individuals and organizations consistent with AAIF and Linux Foundation policies. Members participate as individuals in service of the foundation's mission, rather than as representatives of their employers.

## How the work is organized

The breakouts turn shared problem statements into concrete inputs and deliverables. They coordinate in the main working-group meeting so that terminology, use cases, and architecture evolve together.

| Breakout | Focus | Coordinator or liaison | Working material |
| --- | --- | --- | --- |
| Use Cases | Ground the work in enterprise and consumer scenarios and derive identity and trust requirements. | Wei Chen | [Use Cases working document](https://docs.google.com/document/d/1xvBkd7kCYYvsR86fd4p8rGAi-tekmVuKy9Eiyc0hpPo/edit?tab=t.0) |
| Reference Architecture | Describe the actors, components, trust relationships, and interoperability gaps needed to support agent identity and delegated authority. | Brian Malone | [Reference Architecture working document](https://docs.google.com/document/d/1nu4k_6zBgyEowLphuuaNrn6TnQbgeJm7FMkD7R-EXiA/edit?tab=t.0) |
| Taxonomy coordination | Develop and socialize I&T terminology, and coordinate it with the cross-working-group Taxonomy & Landscape Workstream. | Liaisons: Julianna Mealin and Leonardo Galesky | [I&T Taxonomy whiteboard](https://docs.google.com/document/d/12EAOL69K7cxzN_kMpCoR17gaabJYbsdzlw6cNDdR8HY/edit?tab=t.0#heading=h.3ao8274xwzs8) and [Taxonomy & Landscape onboarding](https://github.com/aaif/ws-taxonomy-landscape/blob/main/ONBOARDING.md) |

Matt Khouzam and Junjie Bu also participate in both I&T and the Taxonomy & Landscape Workstream, but are not designated as I&T taxonomy liaisons.

Working documents are collaborative drafts, not approved specifications. When a proposal becomes stable, move it into this repository through an issue or pull request so it can be reviewed and cited reliably.

## Current technical themes

The group's discussions repeatedly return to these connected themes:

- agent identity, authentication, and provenance;
- delegation and authority chains, including recursive delegation;
- authorization, consent, and risk-based human approval;
- trust evaluation, agent discovery, and registry interoperability;
- human-in-the-loop escalation and evidence of approval;
- audit, accountability, revocation, and cross-domain interoperability.

Current deliverables include an identity taxonomy, critical use cases, a survey of the landscape, and an identity reference architecture. Definitions and architecture should remain consistent with the use cases and should clearly identify gaps that cannot be addressed by existing standards.

## Frequently referenced work

These materials have informed presentations or recurring discussions. They are useful context, not adopted I&T specifications.

- [Agentic Resource Discovery (ARD)](https://github.com/ards-project/ard-spec), presented by Junjie Bu: discovery and federation of agent capabilities and resources.
- [Solving the Identity Crisis for AI Agents](https://www.uber.com/blog/solving-the-agent-identity-crisis/), by Matt Mathew and the Uber Engineering Security team: agent registration, SPIFFE/SPIRE workload attestation, per-hop token exchange, actor chains, and policy enforcement.
- [SPIFFE/SPIRE](https://spiffe.io/docs/latest/spiffe-about/overview/): a strong workload-identity foundation whose use for agents raises additional questions about human delegation semantics, agent-level identity, and portable authority across trust domains. Presenter attribution for the earlier I&T discussion still needs to be confirmed.
- [NVIDIA Secure Agent Workspace reference design](https://docs.nvidia.com/enterprise-reference-architectures/secure-agent-workspace-reference-design/latest/what-is-secure-agent-workspace.html): a layered identity, delegation, and policy-enforcement design evaluated by the group.
- [IETF AI Agent Authentication and Authorization draft](https://datatracker.ietf.org/doc/draft-klrc-aiagent-auth/): related protocol work that helps the group distinguish between existing standards and unresolved gaps.

For proposed follow-up presentations and topics that still need an owner or decision, see [Outstanding Agenda Topics](AGENDA.md).

## Meetings, summaries, recordings, and transcripts

The [running notes](https://docs.google.com/document/d/1JfVIQBbxpMT28poaEyAwnINXRC9ZuLPg5q08G6CjPCM/edit?usp=sharing) are the fastest way to review agendas and written discussion. LFX also stores meeting artifacts:

1. Create or sign in to a Linux Foundation account at [app.lfx.dev](https://app.lfx.dev).
2. Open the Individual Dashboard and select **Meetings**.
3. Select **Past Meetings**, then find the relevant AAIF Identity & Trust meeting by date.
4. Open the available recording, transcript, or AI summary.

Availability depends on the meeting's recording and publication settings. If an expected artifact is missing, ask in the I&T Discord channel or contact [support@aaif.io](mailto:support@aaif.io). The Linux Foundation's [My Meetings documentation](https://docs.linuxfoundation.org/lfx/my-profile/meetings) has screenshots and more detailed navigation instructions.

## Ways to contribute

- Add or refine a use case and identify the trust decisions it requires.
- Review a taxonomy term for technical clarity, boundaries, and cross-working-group impact.
- Map an architecture component to existing specifications and document the remaining gap.
- Volunteer to present relevant implementation experience or standards work.
- Take ownership of an item in the [outstanding agenda](AGENDA.md).
- Open an issue or pull request that turns meeting consensus into a durable repository artifact.

When proposing a topic, include the problem, desired outcome, relevant background links, and the person who can drive the next step. Keep vendor-specific implementations framed as inputs to vendor-neutral conclusions.

## Repository contributions

For a documentation change:

1. Open or identify an issue when the proposal needs discussion.
2. Create a focused branch and edit the relevant Markdown files.
3. Link the issue, meeting notes, or source material in the pull request.
4. Summarize the proposed conclusion and call out unresolved questions.
5. Request review from the relevant breakout coordinator, liaison, or working-group chair.

Questions are welcome in the [I&T Discord channel](https://discord.com/channels/1461090924791595243/1463637083737296979) or on the [mailing list](https://lists.aaif.io/g/wg-identity-trust).
