# AttendanceRecord

[Registration, tickets and attendance](../../ministry/registration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Named or restricted guest observation. Unique counted presence per person and occurrence. Mark present, excused, absent, late or remote only where reliably known. Record room movements or multiple scans separately.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `place_id` | → RegistrationPlace? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `group_id` | → MinistryGroup? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `observed_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `recorded_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source` | code | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `correction_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

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

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### place_id

The target is [RegistrationPlace](RegistrationPlace.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RegistrationPlace·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RegistrationPlace·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RegistrationPlace·MISSING | Queue the missing RegistrationPlace mapping or reject the command before linking. |
| Wrong scope | RegistrationPlace·B01 | Do not attach another church’s RegistrationPlace without a supported exchange and local authority. |
| Target rename | Rename RegistrationPlace·A01 after linking | The existing place_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No place_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### group_id

The target is [MinistryGroup](MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No group_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `AttendanceRecord.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### observed_at

Use unambiguous point in time for `AttendanceRecord.observed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No observed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### source

Use scoped or external reference for `AttendanceRecord.source`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No source at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### correction_reason

Use human-readable text for `AttendanceRecord.correction_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered correction_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No correction_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
