# PassengerBooking

[Facilities, equipment and fleet](../../ministry/resources.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Both stops belong to the journey; leave follows board. Reserve capacity per segment and seat configuration. A child's authority for boarding or handover is checked separately.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `journey_id` | → TransportJourney | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `board_stop_id` | → TransportStop | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `leave_stop_id` | → TransportStop | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `seat_type` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `assistance_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `boarded_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `alighted_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### journey_id

The target is [TransportJourney](TransportJourney.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TransportJourney·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TransportJourney·MISSING | Queue the missing TransportJourney mapping or reject the command before linking. |
| Wrong scope | TransportJourney·B01 | Do not attach another church’s TransportJourney without a supported exchange and local authority. |
| Target rename | Rename TransportJourney·A01 after linking | The existing journey_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No journey_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### board_stop_id

The target is [TransportStop](TransportStop.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TransportStop·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TransportStop·MISSING | Queue the missing TransportStop mapping or reject the command before linking. |
| Wrong scope | TransportStop·B01 | Do not attach another church’s TransportStop without a supported exchange and local authority. |
| Target rename | Rename TransportStop·A01 after linking | The existing board_stop_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No board_stop_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### leave_stop_id

The target is [TransportStop](TransportStop.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TransportStop·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TransportStop·MISSING | Queue the missing TransportStop mapping or reject the command before linking. |
| Wrong scope | TransportStop·B01 | Do not attach another church’s TransportStop without a supported exchange and local authority. |
| Target rename | Rename TransportStop·A01 after linking | The existing leave_stop_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No leave_stop_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seat_type

Use versioned classification or status code for `PassengerBooking.seat_type`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active seat_type code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped seat_type code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No seat_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assistance_ref

Use scoped or external reference for `PassengerBooking.assistance_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified assistance_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped assistance_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No assistance_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `PassengerBooking.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### boarded_at

Use unambiguous point in time for `PassengerBooking.boarded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No boarded_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### alighted_at

Use unambiguous point in time for `PassengerBooking.alighted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No alighted_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
