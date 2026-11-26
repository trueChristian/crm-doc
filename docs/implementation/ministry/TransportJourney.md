# TransportJourney

[Facilities, equipment and fleet](../../ministry/resources.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Recheck vehicle availability, capacity and driver clearance for entire journey. A paid driver or reimbursable mileage references finance separately.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `vehicle_id` | → MinistryVehicle | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `occurrence_id` | → EventOccurrence? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `trip_leg_id` | → TripLeg? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `driver_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `departs_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `returns_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `route_label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `opening_distance` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `closing_distance` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `distance_unit` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### vehicle_id

The target is [MinistryVehicle](MinistryVehicle.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryVehicle·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryVehicle·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryVehicle·MISSING | Queue the missing MinistryVehicle mapping or reject the command before linking. |
| Wrong scope | MinistryVehicle·B01 | Do not attach another church’s MinistryVehicle without a supported exchange and local authority. |
| Target rename | Rename MinistryVehicle·A01 after linking | The existing vehicle_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No vehicle_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### occurrence_id

The target is [EventOccurrence](EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventOccurrence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing occurrence_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No occurrence_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### trip_leg_id

The target is [TripLeg](TripLeg.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TripLeg·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | TripLeg·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | TripLeg·MISSING | Queue the missing TripLeg mapping or reject the command before linking. |
| Wrong scope | TripLeg·B01 | Do not attach another church’s TripLeg without a supported exchange and local authority. |
| Target rename | Rename TripLeg·A01 after linking | The existing trip_leg_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No trip_leg_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### driver_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing driver_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No driver_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### departs_at

Use unambiguous point in time for `TransportJourney.departs_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No departs_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### returns_at

Use unambiguous point in time for `TransportJourney.returns_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No returns_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### route_label

Use human-readable text for `TransportJourney.route_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered route_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No route_label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `TransportJourney.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opening_distance

Use exact decimal measure for `TransportJourney.opening_distance`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No opening_distance provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### closing_distance

Use exact decimal measure for `TransportJourney.closing_distance`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No closing_distance provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### distance_unit

Use versioned classification or status code for `TransportJourney.distance_unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active distance_unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped distance_unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No distance_unit provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PassengerBooking](PassengerBooking.md).`journey_id` | TransportJourney identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TransportStop](TransportStop.md).`journey_id` | TransportJourney identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
