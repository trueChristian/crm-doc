# ShiftExchange

[Volunteers and rotas](../../ministry/volunteers.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many proposals may exist, only one can replace the same active assignment. Keep original and replacement linked.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `original_id` | → VolunteerAssignment | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `candidate_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `requester_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `requested_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `reviewed_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `replacement_id` | → VolunteerAssignment? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### original_id

The target is [VolunteerAssignment](VolunteerAssignment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VolunteerAssignment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VolunteerAssignment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VolunteerAssignment·MISSING | Queue the missing VolunteerAssignment mapping or reject the command before linking. |
| Wrong scope | VolunteerAssignment·B01 | Do not attach another church’s VolunteerAssignment without a supported exchange and local authority. |
| Target rename | Rename VolunteerAssignment·A01 after linking | The existing original_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No original_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### candidate_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing candidate_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No candidate_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### requester_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing requester_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No requester_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_at

Use unambiguous point in time for `ShiftExchange.requested_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No requested_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `ShiftExchange.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### replacement_id

The target is [VolunteerAssignment](VolunteerAssignment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VolunteerAssignment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VolunteerAssignment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VolunteerAssignment·MISSING | Queue the missing VolunteerAssignment mapping or reject the command before linking. |
| Wrong scope | VolunteerAssignment·B01 | Do not attach another church’s VolunteerAssignment without a supported exchange and local authority. |
| Target rename | Rename VolunteerAssignment·A01 after linking | The existing replacement_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No replacement_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
