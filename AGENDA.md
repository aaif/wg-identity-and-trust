# Outstanding Agenda Topics

This file tracks proposed Identity & Trust Working Group presentations and unresolved discussion topics. It complements the [running meeting notes](https://docs.google.com/document/d/1JfVIQBbxpMT28poaEyAwnINXRC9ZuLPg5q08G6CjPCM/edit?usp=sharing), which remain the record of scheduled agendas, discussion, and decisions.

## How to use this list

- Add a topic before a meeting and identify an owner who can drive the next step.
- State the desired outcome: information sharing, design feedback, a documented decision, or a follow-up artifact.
- Update the status when the item is scheduled, discussed, converted to an issue or pull request, or closed.
- Link the resulting notes or artifact so future participants can find the outcome.

## Presentation queue

| Presenter or organization | Proposed topic | Desired outcome | Owner / next step | Status |
| --- | --- | --- | --- | --- |
| Matt Mathew / Uber | [Uber's production agent identity architecture](https://www.uber.com/blog/solving-the-agent-identity-crisis/): agent registration, SPIFFE/SPIRE attestation, actor chains, per-hop token exchange, and enforcement. | Identify reusable patterns, deployment assumptions, and standards gaps relevant to the I&T reference architecture. | Confirm invitation and meeting date. | Proposed |
| Empire Labs | Agent trust, audit, and orchestration experience; exact presentation scope to be confirmed with the speaker. | Capture implementation lessons and determine which findings should feed the use cases, taxonomy, or reference architecture. | Identify the speaker/contact and agree on scope. | Proposed |
| SPIFFE/SPIRE practitioner (TBD) | Follow-up on the boundary between workload identity and agent identity, especially human delegation, agent-level identity, and authority across trust domains. | Document where existing workload-identity mechanisms are sufficient and where agent-specific semantics or profiles are needed. | Confirm the earlier presenter or invite another practitioner. | Proposed |

## Working discussion queue

| Topic | Desired outcome | Suggested owner | Status |
| --- | --- | --- | --- |
| OAuth 2.0 baseline for agent authorization | Decide whether to recommend an OAuth 2.0 profile for presenting agent authorization across platforms, while leaving local policy enforcement out of scope. | Reference Architecture breakout | Needs WG discussion |
| Agent identity primitive | Define the minimum information that represents an agent as a first-class actor distinct from its user, application, and workload. | Reference Architecture + Taxonomy | In progress |
| Delegation-chain constraints | Align on attenuation, audience, lifetime, revocation, and evidence requirements for human-to-agent and recursive agent-to-agent delegation. | Use Cases + Reference Architecture | In progress |
| Action Record boundary | Clarify the relationship among an action record, consent receipt, audit log, and operational trace; coordinate with Observability & Traceability. | Taxonomy liaisons | In progress |
| ARD and registry interoperability | Review how [Agentic Resource Discovery](https://github.com/ards-project/ard-spec) addresses discovery and federation, and record any identity/trust gaps. | Junjie Bu / volunteer | Follow-up needed |
| Cross-working-group coordination | Identify concrete handoffs to Security & Privacy, Observability & Traceability, Agentic Commerce, and Taxonomy & Landscape. | WG chairs and liaisons | Recurring |

## Completed topics

Move completed items here with the meeting date and a link to the resulting notes, issue, pull request, or published artifact.

| Date | Topic | Outcome |
| --- | --- | --- |
| _YYYY-MM-DD_ | _Example_ | _Link to notes or artifact_ |
