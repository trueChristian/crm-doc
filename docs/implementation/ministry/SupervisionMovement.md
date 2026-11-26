# SupervisionMovement

[Children and supervised handover](../../ministry/child-check-in.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

The sending team remains responsible until receipt is acknowledged. Competing moves, closed destination and excess capacity block acceptance.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `check_in_id` | → ChildCheckIn | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `from_session_id` | → SupervisedSession | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `to_session_id` | → SupervisedSession | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `requested_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `requested_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `accepted_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `accepted_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### check_in_id

The target is [ChildCheckIn](ChildCheckIn.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ChildCheckIn·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ChildCheckIn·MISSING | Queue the missing ChildCheckIn mapping or reject the command before linking. |
| Wrong scope | ChildCheckIn·B01 | Do not attach another church’s ChildCheckIn without a supported exchange and local authority. |
| Target rename | Rename ChildCheckIn·A01 after linking | The existing check_in_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No check_in_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_session_id

The target is [SupervisedSession](SupervisedSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupervisedSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SupervisedSession·MISSING | Queue the missing SupervisedSession mapping or reject the command before linking. |
| Wrong scope | SupervisedSession·B01 | Do not attach another church’s SupervisedSession without a supported exchange and local authority. |
| Target rename | Rename SupervisedSession·A01 after linking | The existing from_session_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No from_session_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### to_session_id

The target is [SupervisedSession](SupervisedSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupervisedSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SupervisedSession·MISSING | Queue the missing SupervisedSession mapping or reject the command before linking. |
| Wrong scope | SupervisedSession·B01 | Do not attach another church’s SupervisedSession without a supported exchange and local authority. |
| Target rename | Rename SupervisedSession·A01 after linking | The existing to_session_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No to_session_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_at

Use unambiguous point in time for `SupervisionMovement.requested_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No requested_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing requested_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No requested_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accepted_at

Use unambiguous point in time for `SupervisionMovement.accepted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No accepted_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### accepted_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing accepted_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No accepted_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `SupervisionMovement.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
