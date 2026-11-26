# PersonMerge

[Personal register and identity resolution](../../people/personal-register.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Person-specific field choices, conflicts and case-owner acknowledgments are the evidence/dependency plan for the canonical MergeDecision. Application, aliases and restoration use one decision ID. A reversal is a compensating MergeDecision linked by reversed_by_ref.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | = MergeDecision.id | Projected from MergeDecision; keep source optionality | [alias](../value-conventions.md#alias) |
| `review_id` | → DuplicateCandidate | Projected from MergeDecision; keep source optionality | [relation](../value-conventions.md#relation) |
| `surviving_person_id` | = survivor_ref | Projected from MergeDecision; keep source optionality | [alias](../value-conventions.md#alias) |
| `absorbed_person_id` | = losing_ref | Projected from MergeDecision; keep source optionality | [alias](../value-conventions.md#alias) |
| `approved_by` | → UserAccount? | Projected from MergeDecision; keep source optionality | [relation](../value-conventions.md#relation) |
| `applied_at` | instant? | Projected from MergeDecision; keep source optionality | [instant](../value-conventions.md#instant) |
| `reversal_decision_id` | = reversed_by_ref? | Projected from MergeDecision; keep source optionality | [alias](../value-conventions.md#alias) |
| `reconciliation_summary` | restricted text | Projected from MergeDecision; keep source optionality | [protected](../value-conventions.md#protected) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Authoritative source: `MergeDecision.id`. Record one change at that owner and re-evaluate derived access.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MergeDecision.id | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Proposed view change | Try to change id in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### review_id

The target is [DuplicateCandidate](../platform/DuplicateCandidate.md). Resolve the identifier in the approved scope before using its fields.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DuplicateCandidate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DuplicateCandidate·MISSING | Queue the missing DuplicateCandidate mapping or reject the command before linking. |
| Wrong scope | DuplicateCandidate·B01 | Do not attach another church’s DuplicateCandidate without a supported exchange and local authority. |
| Target rename | Rename DuplicateCandidate·A01 after linking | The existing review_id keeps the same identity and historic documents retain their original wording. |
| Proposed view change | Try to change review_id in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### surviving_person_id

Authoritative source: `survivor_ref`. Record one change at that owner and re-evaluate derived access.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | survivor_ref | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Proposed view change | Try to change surviving_person_id in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### absorbed_person_id

Authoritative source: `losing_ref`. Record one change at that owner and re-evaluate derived access.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | losing_ref | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Proposed view change | Try to change absorbed_person_id in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Proposed view change | Try to change approved_by in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### applied_at

Use unambiguous point in time for `PersonMerge.applied_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Proposed view change | Try to change applied_at in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### reversal_decision_id

Authoritative source: `reversed_by_ref?`. Record one change at that owner and re-evaluate derived access.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | reversed_by_ref | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Proposed view change | Try to change reversal_decision_id in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

### reconciliation_summary

Use restricted value or protected content reference for `PersonMerge.reconciliation_summary`. Keep value and purpose together; apply field-level authority to projections.
This is an owner-backed view. Compare the corresponding value at MergeDecision; no independent change or second approval is permitted here.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted reconciliation_summary supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Proposed view change | Try to change reconciliation_summary in the local view | Route the operation to MergeDecision and refresh the permitted projection from the accepted revision. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PersonMergeItem](PersonMergeItem.md).`merge_id` | PersonMerge identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
