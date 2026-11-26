# ReviewDecision

[Complaints, whistleblowing and grievances](../../assurance/complaints-and-grievances.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Versioned findings, remedies and recipient-specific outcomes. A volunteer scheduling change, employment decision or financial correction follows its own authorized workflow. The docket alone grants no such power.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `docket_id` | → ReviewDocket | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `decided_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `decided_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `issue_outcomes_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `reasons` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `remedy_summary` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `disclosure_versions_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `appeal_deadline_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `follows_decision_id` | → ReviewDecision? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ReviewDecision.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReviewDecision·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### docket_id

The target is [ReviewDocket](ReviewDocket.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReviewDocket·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReviewDocket·MISSING | Queue the missing ReviewDocket mapping or reject the command before linking. |
| Wrong scope | ReviewDocket·B01 | Do not attach another church’s ReviewDocket without a supported exchange and local authority. |
| Target rename | Rename ReviewDocket·A01 after linking | The existing docket_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No docket_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decided_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing decided_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No decided_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decided_at

Use unambiguous point in time for `ReviewDecision.decided_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No decided_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issue_outcomes_ref

Use scoped or external reference for `ReviewDecision.issue_outcomes_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified issue_outcomes_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped issue_outcomes_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No issue_outcomes_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reasons

Use restricted value or protected content reference for `ReviewDecision.reasons`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted reasons supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No reasons at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### remedy_summary

Use restricted value or protected content reference for `ReviewDecision.remedy_summary`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted remedy_summary supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No remedy_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disclosure_versions_ref

Use scoped or external reference for `ReviewDecision.disclosure_versions_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified disclosure_versions_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped disclosure_versions_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No disclosure_versions_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### appeal_deadline_at

Use unambiguous point in time for `ReviewDecision.appeal_deadline_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No appeal_deadline_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### follows_decision_id

The target is [ReviewDecision](ReviewDecision.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReviewDecision·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReviewDecision·MISSING | Queue the missing ReviewDecision mapping or reject the command before linking. |
| Wrong scope | ReviewDecision·B01 | Do not attach another church’s ReviewDecision without a supported exchange and local authority. |
| Target rename | Rename ReviewDecision·A01 after linking | The existing follows_decision_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No follows_decision_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CaseAppeal](CaseAppeal.md).`decision_id` | ReviewDecision identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CaseAppeal](CaseAppeal.md).`outcome_id` | ReviewDecision identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RemedyVerification](RemedyVerification.md).`decision_id` | ReviewDecision identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewDecision](ReviewDecision.md).`follows_decision_id` | ReviewDecision identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
