# PersonMerge

[Personal register and identity resolution](../../people/personal-register.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Person-specific field choices, conflicts and case-owner acknowledgments are the evidence/dependency plan for the canonical MergeDecision. Application, aliases and restoration use one decision ID. A reversal is a compensating MergeDecision linked by reversed_by_ref.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | = MergeDecision.id | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `review_id` | → DuplicateCandidate | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `surviving_person_id` | = survivor_ref | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `absorbed_person_id` | = losing_ref | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `approved_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `applied_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `reversal_decision_id` | = reversed_by_ref? | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `reconciliation_summary` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Authoritative source: `MergeDecision.id`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MergeDecision.id | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### review_id

The target is [DuplicateCandidate](../platform/DuplicateCandidate.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DuplicateCandidate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DuplicateCandidate·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DuplicateCandidate·MISSING | Queue the missing DuplicateCandidate mapping or reject the command before linking. |
| Wrong scope | DuplicateCandidate·B01 | Do not attach another church’s DuplicateCandidate without a supported exchange and local authority. |
| Target rename | Rename DuplicateCandidate·A01 after linking | The existing review_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No review_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### surviving_person_id

Authoritative source: `survivor_ref`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | survivor_ref | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace surviving_person_id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### absorbed_person_id

Authoritative source: `losing_ref`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | losing_ref | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace absorbed_person_id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No approved_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### applied_at

Use unambiguous point in time for `PersonMerge.applied_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No applied_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reversal_decision_id

Authoritative source: `reversed_by_ref?`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | reversed_by_ref | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Absent in intake | No reversal_decision_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reconciliation_summary

Use restricted value or protected content reference for `PersonMerge.reconciliation_summary`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted reconciliation_summary supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No reconciliation_summary at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PersonMergeItem](PersonMergeItem.md).`merge_id` | PersonMerge identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
