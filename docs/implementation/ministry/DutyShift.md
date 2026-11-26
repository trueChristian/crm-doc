# DutyShift

[Volunteers and rotas](../../ministry/volunteers.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One occurrence can have many shifts, including setup and teardown outside its public hours. The shift belongs to one organization and its campus location is explicit.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `position_id` | → ServicePosition | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `room_booking_id` | → RoomBooking? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `starts_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `ends_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `required_count` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `standby_count` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `lead_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### occurrence_id

The target is [EventOccurrence](EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventOccurrence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing occurrence_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No occurrence_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### position_id

The target is [ServicePosition](ServicePosition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServicePosition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ServicePosition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ServicePosition·MISSING | Queue the missing ServicePosition mapping or reject the command before linking. |
| Wrong scope | ServicePosition·B01 | Do not attach another church’s ServicePosition without a supported exchange and local authority. |
| Target rename | Rename ServicePosition·A01 after linking | The existing position_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No position_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### room_booking_id

The target is [RoomBooking](RoomBooking.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RoomBooking·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RoomBooking·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RoomBooking·MISSING | Queue the missing RoomBooking mapping or reject the command before linking. |
| Wrong scope | RoomBooking·B01 | Do not attach another church’s RoomBooking without a supported exchange and local authority. |
| Target rename | Rename RoomBooking·A01 after linking | The existing room_booking_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No room_booking_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### starts_at

Use unambiguous point in time for `DutyShift.starts_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No starts_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_at

Use unambiguous point in time for `DutyShift.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No ends_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### required_count

Use whole-number measure for `DutyShift.required_count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No required_count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### standby_count

Use whole-number measure for `DutyShift.standby_count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No standby_count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### lead_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing lead_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No lead_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [VolunteerAssignment](VolunteerAssignment.md).`shift_id` | DutyShift identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
