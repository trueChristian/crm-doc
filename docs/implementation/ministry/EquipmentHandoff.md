# EquipmentHandoff

[Facilities, equipment and fleet](../../ministry/resources.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Preserve each issue, partial return, transfer or loss report. Returned quantity cannot exceed outstanding quantity. Disputed damage requires review.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `reservation_id` | → EquipmentReservation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `action` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `occurred_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `giver_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `receiver_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `condition` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `note` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `recorded_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### reservation_id

The target is [EquipmentReservation](EquipmentReservation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EquipmentReservation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EquipmentReservation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EquipmentReservation·MISSING | Queue the missing EquipmentReservation mapping or reject the command before linking. |
| Wrong scope | EquipmentReservation·B01 | Do not attach another church’s EquipmentReservation without a supported exchange and local authority. |
| Target rename | Rename EquipmentReservation·A01 after linking | The existing reservation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reservation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### action

Use versioned classification or status code for `EquipmentHandoff.action`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active action code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped action code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No action at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `EquipmentHandoff.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### occurred_at

Use unambiguous point in time for `EquipmentHandoff.occurred_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No occurred_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### giver_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing giver_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No giver_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### receiver_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing receiver_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No receiver_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### condition

Use versioned classification or status code for `EquipmentHandoff.condition`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active condition code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped condition code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No condition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### note

Use human-readable text for `EquipmentHandoff.note`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered note in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recorded_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing recorded_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No recorded_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
