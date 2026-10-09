# Outstanding Agenda Topics

This file tracks proposed Identity & Trust Working Group presentations and unresolved discussion topics. It complements the [running meeting notes](https://docs.google.com/document/d/1JfVIQBbxpMT28poaEyAwnINXRC9ZuLPg5q08G6CjPCM/edit?usp=sharing), which remain the record of scheduled agendas, discussion, and decisions.

## How to use this list

- Add a topic before a meeting and identify an owner who can drive the next step.
- State the desired outcome: information sharing, design feedback, a documented decision, or a follow-up artifact.
- Update the status when the item is scheduled, discussed, converted to an issue or pull request, or closed.
- Link the resulting notes or artifact so future participants can find the outcome.

## Presentation queue

- **A human-backed agent credential run against the delegated-authority cases** - Owner: Marc Molas (MintID). Desired outcome: design feedback for the Critical Use Cases requirements and for the Reference Architecture text on accountability, revocation and principal traceability (§3.x, §3.5, §5), and a view on whether conformance answers must state their residual risk. Content: the delegated-authority cases proposed on the list, run against one implementation with the known gap of each; revocation measured per path against declared bounds; a relying party that learns that an accountable, verified principal stands behind the agent, within scope, without learning who. Evidence: issue #13 (MintID row), the records under `test-harness/trace/records/` at `public-v2026-10-08.2` (gitlab.com/mintid/mintid), a third-party run on agentrust-io/integrations #287, and the independent reproduction announced on the list by ALIGN/bitgrit from 15 October. Scope: implementation input; operator records except where stated; no AAIF conformance claim. 20 minutes plus questions. Proposed date: 29 October or 5 November 2026. Status: proposed.
