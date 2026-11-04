# Authority at dispatch and committed effect

Status: proposed. Comparison record for [issue 13](https://github.com/aaif/wg-identity-and-trust/issues/13).

## Contract

Every trace submitted for this comparison writes:

```json
"contractId": "https://probityai.github.io/agent-evidence-observer/contract/authority-at-dispatch/v1"
```

A reader refuses a trace that omits the identifier or names another version. A change to the required meaning of any field is a new version. The fields and their required meaning are in [CONTRACT.md](https://github.com/probityai/probity/blob/8892c6acdf4776ceecbbdfefe48026f316c6c1e0/packages/agent-evidence-observer/interop/authority-unreachable-2026-10-03/CONTRACT.md).

Authority evidence carries `evidenceAgeSeconds` (decision time minus the signed observation time) and `freshnessLimitSeconds` (the deployed limit), which Imran Siddique asked the comparison to retain on 3 October ([message 26](https://lists.aaif.io/g/wg-identity-trust/message/26)). A field a trace leaves unfilled is marked `not_applicable`, `not_emitted` or `not_measured`, kept apart as he asked on 6 October.

## Cases

| Case | Expected invariant | Reference cases |
| --- | --- | --- |
| 1. Delegator revoked after downstream delegation | No dispatch after the revocation reaches the enforcement point | `approver-revoked-at-dispatch`, `revoked-between-intent-and-effect`, `effect-then-authority-revoked` |
| 2. Valid delegation for the wrong object or action | Dispatched bytes equal the approved digest | `media-bytes-mutated`, `platform-content-mutated`, `catalogue-mutated`, `destination-mutated` |
| 3. Stale revocation information | Evidence older than the deployed limit is refused | `authority-evidence-stale` |
| 4. Escalation authority unavailable | No new authority from unavailability | `unreachable-with-prior-fallback`, `unreachable-no-fallback` |
| 5. Authority amplified across hops | Each hop's scope is a subset of the hop before | `delegation-hop-amplified` |
| 6. Identity valid, authority expired | Grant expiry and the original deadline bound dispatch | `fallback-expired`, `late-approval-for-expired-request` |

The six cases are the ones proposed in [message 14](https://lists.aaif.io/g/wg-identity-trust/message/14). Case 7 (the delegation chain as a surveillance graph) and case 8 (a revocation issued in error, or disputed) were added on 5 October ([message 32](https://lists.aaif.io/g/wg-identity-trust/message/32)) and have no reference case yet.

## Implementation rows

| Implementation | Record | State |
| --- | --- | --- |
| MintID | Operator traces at `public-v2026-10-07` and `public-v2026-10-08.2`, and an independent testnet run of the same trace at `public-v2026-10-08.2` | Decisions measured; committed effect outside the implementation |
| Proofable | `aaif-e1217327a-20261008` at `proofable/docs` `9851059` | Decisions measured; 11 disclosed envelopes verify from the published bytes |
| Alakris | `aaif-publication-reference` `ebd9dcf` and its rerun of the reference cases | Reference cases reproduced; deployed path not measured |

## Running the check

The [workflow](../.github/workflows/authority-at-dispatch.yml) installs the reader at a pinned commit, runs the reference cases, and refuses any trace under `catalogue/authority-at-dispatch/traces/` that does not carry the contract identifier.
