# Delegation lifecycle test cases

Status: proposed. Test cases for the two use cases in
[issue 18](https://github.com/aaif/wg-identity-and-trust/issues/18): disputed
revocation across a delegation tree, and re-registration under a new identifier.

Each case asks one question: does this presenter hold this delegated authority at
the time the relying party observed the presentation? A case is a directory of
signed records (identifier registrations, grants, revocations, disputes,
resolutions, identifier links, retirements) and one presentation signed by the
presenter and countersigned by the relying party, with the policy that judges
them in `case.json`. Every record is a DSSE envelope signed with Ed25519 test
keys anyone can re-derive. [INDEX.md](INDEX.md) gives every case's situation,
expected outcome and rule; `MANIFEST.json` holds the same outcomes for a
program to read.

The cases are copied byte for byte from
[agent-evidence-vectors](https://github.com/probityai/agent-evidence-vectors/tree/v0.19.0/vectors-delegation-lifecycle)
release `v0.19.0`. The [workflow](../../.github/workflows/delegation-lifecycle.yml)
installs the verifier `aee-verify` pinned to that release and checks that every
case gets its expected outcome. To run it yourself:

```sh
go install github.com/probityai/agent-evidence-vectors/cmd/aee-verify@v0.19.0
aee-verify test-cases/delegation-lifecycle
```

To test another verifier, run it over each `cases/<id>/` directory and compare
its answer with `expected` in `MANIFEST.json`.

## Revocation across a delegation tree

An organisation delegates to a planner, which delegates to a worker and a
sibling; the worker delegates to a sub-worker.

| Case | Outcome | What it tests |
| --- | --- | --- |
| `tree-chain-valid` | accept | the baseline chain, nothing revoked |
| `tree-parent-revoked-child-presented` | reject | the planner's grant is revoked and the worker presents its child grant afterwards |
| `tree-child-presented-before-revocation` | accept | the time rule: a revocation applies from its `effective_at`, against the relying party's `observed_at` |
| `tree-sibling-of-revoked-child` | accept | revoking the worker leaves its sibling's grant standing |
| `tree-grandchild-under-revoked-parent` | reject | the cascade reaches two levels down |
| `tree-child-revocation-keeps-parent` | accept | revoking a child does not revoke its parent |
| `tree-revocation-backdated` | reject | a revocation issued late applies from its stated effective time |
| `tree-revocation-without-standing` | accept | a revocation signed by someone outside the chain above the grant is ignored |
| `tree-revocation-forged` | accept | a revocation whose signature does not verify stops nothing |
| `tree-revocation-incomplete` | reject | a revocation without stated grounds still stops authority, and the refusal says so |
| `tree-conflicting-revocations` | reject | of two revocations with standing, the earliest effective time applies |
| `tree-dispute-open` | reject | a worker cut off by the cascade disputes; the dispute does not suspend the revocation, and the refusal says it is open |
| `tree-dispute-confirmed` | reject | the dispute is resolved by confirming the revocation |
| `tree-resolution-without-standing` | reject | the disputing worker cannot resolve its own dispute |
| `tree-dispute-restored-by-new-grant` | accept | a dispute resolved in the planner's favour restores it through a replacement grant |
| `tree-revoked-grant-after-restoration` | reject | the revoked grant itself stays revoked |
| `tree-cascade-victim-after-restoration` | reject | the worker's old grant still names the revoked parent |
| `tree-cascade-victim-reissued` | accept | the worker's grant re-issued under the replacement |
| `tree-grant-tampered` | reject | a grant edited after signing |
| `tree-presentation-unattested` | reject | a presentation the relying party did not countersign |
| `tree-chain-skips-a-grant` | reject | a chain with a grant missing |
| `tree-root-not-trusted` | reject | a top-level grant from a principal the policy does not trust |
| `tree-record-not-json` | no verdict | a record that is not JSON |

## Re-registration under a new identifier

An organisation grants authority to `agent-v1`, which is re-registered as
`agent-v2`.

| Case | Outcome | What it tests |
| --- | --- | --- |
| `rereg-linked-successor` | accept | a link signed by the old key, the new key and the registry carries the grant to the new identifier |
| `rereg-no-link` | reject | a new identifier with no link holds nothing |
| `rereg-link-signed-by-wrong-key` | reject | the new identifier signs in the old identifier's place |
| `rereg-link-not-registry-attested` | reject | a link without the registry's signature |
| `rereg-two-old-one-new` | reject | two old identifiers linked to one new one |
| `rereg-one-old-two-new` | reject | one old identifier linked to two new ones |
| `rereg-link-after-old-revoked` | reject | a link made after the registry revoked the old identifier for key compromise |
| `rereg-chain-old-middle-new` | accept | links followed hop by hop, old to middle to new |
| `rereg-chain-middle-revoked` | reject | the middle identifier was revoked before its onward link |
| `rereg-old-presents-after-retirement` | reject | the old identifier presents after the registry retired it |
| `rereg-old-presents-before-retirement` | accept | the old identifier presents after the link and before its retirement |
| `rereg-revocation-follows-link` | reject | a revocation of the grant reaches the successor |

## Recovery after a lost or compromised key (proposed)

A link needs the old key's signature, so it cannot be made when that key is lost
or compromised at redeployment ([issue 18](https://github.com/aaif/wg-identity-and-trust/issues/18)).
These cases put that path in a separate record, the recovery record, which is
signed by the registry and the Responsible entity and counts only when both
identifiers were registered to that entity with one software attestation digest.
It carries the old identifier's adverse records forward and never a grant. When
a registration matches a retired agent and asks for no recovery, the registry
records a succession on its own signature, with the same effect. These
cases are not copied into this directory: the `recovery` job in the
[workflow](../../.github/workflows/delegation-lifecycle.yml) fetches
agent-evidence-vectors at release v0.24.0 and runs that release's
verifier over that release's corpus. Their records, rules and expected outcomes
are in
[INDEX.md at that release](https://github.com/probityai/agent-evidence-vectors/blob/v0.24.0/vectors-delegation-lifecycle/INDEX.md#recovery-after-a-lost-or-compromised-key).

| Case | Outcome | What it tests |
| --- | --- | --- |
| `recovery-regrant` | accept | after a recovery the issuer grants the new identifier again |
| `recovery-grant-not-carried` | reject | the new identifier presents the old identifier's grant through a recovery |
| `recovery-registry-only` | reject | a recovery signed by the registry and not the Responsible entity |
| `recovery-software-mismatch` | reject | the two registrations carry different software attestation digests |
| `recovery-after-compromise-no-revival` | reject | a recovery after a compromise revocation does not restore the revoked authority |
| `recovery-after-compromise-regrant` | accept | a new grant after a compromise recovery, accepted with the compromise in the history |
| `recovery-history-follows` | accept | an earlier revocation and its confirmed dispute resolve from the successor |
| `recovery-unclaimed-succession` | accept | the registry records a succession for a re-registration that makes no recovery claim, and the history follows |
| `recovery-unclaimed-unrecorded` | reject | the same re-registration with no succession record drops the history |
| `recovery-new-agent-asserted` | accept | Proposed: the Responsible entity asserts the agent is new; the assertion is recorded and the history still follows, marked contested |
| `recovery-successor-responsible` | accept | a successor Responsible entity signs the recovery under a recorded responsible succession |
| `recovery-successor-responsible-unrecorded` | reject | the same recovery with no responsible-succession record |

To run them yourself:

```sh
go install github.com/probityai/agent-evidence-vectors/cmd/aee-verify@v0.24.0
aee-verify "$(go mod download -json github.com/probityai/agent-evidence-vectors@v0.24.0 | jq -r .Dir)/vectors-delegation-lifecycle"
```

## Sub-agents bound to the parent's lifespan (proposed)

Use case B asks how succession interacts with sub-agents, whose identifiers are
bound to the parent's lifespan. In these cases the registry registers a
sub-agent with a `parent`, and the sub-agent ends when the registry retires or
revokes that parent. A recovery or succession of the parent carries history,
never the parent's grants or its sub-agents. The successor's new sub-agent holds
authority only through new grants, follows the old sub-agent through a succession
record as history only, and carries the history of its parent's predecessor. The
`recovery` job runs them from the same release; their records and rules are in
[INDEX.md at that release](https://github.com/probityai/agent-evidence-vectors/blob/v0.24.0/vectors-delegation-lifecycle/INDEX.md#sub-agents-bound-to-the-parents-lifespan).

| Case | Outcome | What it tests |
| --- | --- | --- |
| `subagent-parent-active` | accept | a sub-agent holds its grant while its parent is active |
| `subagent-parent-retired` | reject | the parent is retired and the sub-agent presents unrevoked grants |
| `subagent-respawned-after-parent-recovery` | accept | after the parent's compromise recovery, the successor's new sub-agent holds new grants and carries the parent's history |
| `subagent-not-carried-by-parent-recovery` | reject | the old sub-agent presents after its parent was recovered to a successor |
| `subagent-succession-history-only` | accept | the old sub-agent's adverse records resolve from the new one through the registry's succession record |
| `subagent-succession-grant-not-carried` | reject | the new sub-agent presents the grants made to the old one |
| `subagent-respawn-unrecorded` | reject | a matching sub-agent registered under the successor with no succession record |

## Where the rules come from

Standing, cascade and irreversibility follow the
[UCAN revocation specification](https://github.com/ucan-wg/revocation): the issuer
of a grant, or any issuer above it in the chain, may revoke it; a revocation
breaks every chain through the revoked grant and no other; and a revocation is
never undone, so a restoration is a new grant. For the disputed revocation, these
cases state the choice the use case asks a design to state: containment over
recoverability.

Rules with no precedent are marked `Proposed:` in `INDEX.md`: that a dispute does
not suspend a revocation, that a resolution needs standing, that a restoration
does not cascade, that a revocation applies from its stated effective time, that
a revocation without grounds still stops authority, that links are one to one,
and that an old identifier stays usable until it is retired. These are the rules
the group can change; each change moves the outcome of the cases that name it.
