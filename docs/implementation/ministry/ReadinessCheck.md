# ReadinessCheck

[Operational readiness, interruptions and review](../../ministry/readiness.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One outcome per applicable criterion and briefing revision. Pending, passed, failed or inapplicable with approved reason. A mandatory unmet item with no authorized alternative prevents a ready decision.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `briefing_id` | → OperationalBriefing | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `criterion_id` | → ReadinessCriterion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `owner_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `due_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `result` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `observed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `reviewed_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `exception_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### briefing_id

The target is [OperationalBriefing](OperationalBriefing.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OperationalBriefing·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OperationalBriefing·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OperationalBriefing·MISSING | Queue the missing OperationalBriefing mapping or reject the command before linking. |
| Wrong scope | OperationalBriefing·B01 | Do not attach another church’s OperationalBriefing without a supported exchange and local authority. |
| Target rename | Rename OperationalBriefing·A01 after linking | The existing briefing_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No briefing_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### criterion_id

The target is [ReadinessCriterion](ReadinessCriterion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReadinessCriterion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ReadinessCriterion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ReadinessCriterion·MISSING | Queue the missing ReadinessCriterion mapping or reject the command before linking. |
| Wrong scope | ReadinessCriterion·B01 | Do not attach another church’s ReadinessCriterion without a supported exchange and local authority. |
| Target rename | Rename ReadinessCriterion·A01 after linking | The existing criterion_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No criterion_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No owner_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### due_at

Use unambiguous point in time for `ReadinessCheck.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No due_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### result

Use versioned classification or status code for `ReadinessCheck.result`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active result code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped result code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### observed_at

Use unambiguous point in time for `ReadinessCheck.observed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No observed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### exception_ref

Use scoped or external reference for `ReadinessCheck.exception_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified exception_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped exception_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No exception_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
