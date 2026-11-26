# RoomStay

[Children and supervised handover](../../ministry/child-check-in.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One check-in has many stays. At most one active room and one designated responsible staff team per child. Preserve prior rooms.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `check_in_id` | → ChildCheckIn | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `session_id` | → SupervisedSession | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `entered_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `received_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `left_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `sent_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `movement_reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

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

### session_id

The target is [SupervisedSession](SupervisedSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupervisedSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SupervisedSession·MISSING | Queue the missing SupervisedSession mapping or reject the command before linking. |
| Wrong scope | SupervisedSession·B01 | Do not attach another church’s SupervisedSession without a supported exchange and local authority. |
| Target rename | Rename SupervisedSession·A01 after linking | The existing session_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No session_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### entered_at

Use unambiguous point in time for `RoomStay.entered_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No entered_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### received_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing received_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No received_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### left_at

Use unambiguous point in time for `RoomStay.left_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No left_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### sent_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing sent_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No sent_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### movement_reason

Use versioned classification or status code for `RoomStay.movement_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active movement_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped movement_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No movement_reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
